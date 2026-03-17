# Building an Import Adapter

This guide is for plugin developers who want to add import support for a new source platform.

## The ImportAdapter interface

Your adapter class must implement `Escalated\Laravel\Contracts\ImportAdapter`:

```php
interface ImportAdapter
{
    /** Unique slug, e.g. "zendesk" */
    public function name(): string;

    /** Human-readable name, e.g. "Zendesk" */
    public function displayName(): string;

    /**
     * Fields required for authentication.
     * Each element: ['name' => string, 'label' => string, 'type' => 'text'|'password'|'url', 'help' => string]
     */
    public function credentialFields(): array;

    /** Validate credentials by making a test API call. */
    public function testConnection(array $credentials): bool;

    /** Ordered list of importable entity types. */
    public function entityTypes(): array;

    /** Default field mappings for an entity type. */
    public function defaultFieldMappings(string $entityType): array;

    /** Available source fields for an entity type (fetched from API using credentials). */
    public function availableSourceFields(string $entityType, array $credentials): array;

    /** Extract a batch of records. Returns null cursor in ExtractResult when exhausted. */
    public function extract(string $entityType, array $credentials, ?string $cursor): ExtractResult;
}
```

## ExtractResult format

Every call to `extract()` must return an `ExtractResult`:

```php
class ExtractResult
{
    public function __construct(
        /** Normalized records as associative arrays */
        public readonly array $records,
        /** Next cursor value, null when exhausted */
        public readonly ?string $cursor,
        /** Estimated total records, if available from API */
        public readonly ?int $totalCount = null,
    ) {}
}
```

Return `null` for `$cursor` to signal that the entity type is fully extracted. The framework will then move on to the next entity type in the list returned by `entityTypes()`.

## Registering the adapter

In your plugin's `Plugin.php`, register your adapter using the `import.adapters` filter hook:

```php
use YourNamespace\YourImportAdapter;

escalated_add_filter('import.adapters', function (array $adapters) {
    $adapters[] = new YourImportAdapter();
    return $adapters;
}, 10);
```

The framework collects all registered adapters and makes them available in the import wizard and CLI.

## Entity types and dependency order

Return entity types from `entityTypes()` in dependency order. The framework imports them in the order you specify; later types can rely on earlier types already being in the database.

Recommended order:

```php
public function entityTypes(): array
{
    return ['agents', 'tags', 'custom_fields', 'departments', 'contacts', 'tickets', 'replies', 'attachments'];
}
```

Not all entity types are required. Omit any that your source platform does not support. For example, if the platform has no custom fields, leave `'custom_fields'` out.

## Cursor-based pagination pattern

The `extract()` method is called repeatedly by the framework until `cursor` is `null`. Your adapter decides the cursor format — it just needs to be a string that encodes enough state to resume the next batch.

Simple page-number cursor:

```php
public function extract(string $entityType, array $credentials, ?string $cursor): ExtractResult
{
    $page = $cursor !== null ? (int) $cursor : 1;

    $data = $this->client->getPage($entityType, $page);

    $records = array_map([$this, 'normalize'], $data['items'] ?? []);
    $nextCursor = count($data['items'] ?? []) > 0 ? (string) ($page + 1) : null;

    return new ExtractResult($records, $nextCursor, $data['total'] ?? null);
}
```

For replies that must be fetched per-ticket, use a compound cursor. See the Zendesk adapter for an example using the `idx:N` / `tid:TICKET_ID|PAGE_URL` pattern, and the `ImportSourceMap` model to iterate over already-imported ticket IDs.

## Normalized record formats

All records are plain associative arrays. The required keys for each entity type are described below.

### agents

```php
[
    'source_id' => '12345',        // string — ID in the source system
    'name'      => 'Jane Doe',
    'email'     => 'jane@example.com',
    'role'      => 'agent',        // 'agent' or 'admin'
]
```

### tags

```php
[
    'source_id' => 'billing',      // string — often the tag name itself
    'name'      => 'billing',
]
```

### custom_fields

```php
[
    'source_id' => '67890',
    'name'      => 'Account tier',
    'type'      => 'select',       // text | textarea | number | checkbox | date | select | multiselect
    'options'   => ['Free', 'Pro', 'Enterprise'],  // for select/multiselect only
]
```

### departments

```php
[
    'source_id' => '111',
    'name'      => 'Billing',
]
```

### contacts

```php
[
    'source_id' => '222',
    'name'      => 'John Smith',
    'email'     => 'john@example.com',
]
```

### tickets

```php
[
    'source_id'            => '333',
    'title'                => 'Cannot log in',
    'status'               => 'open',              // open | in_progress | waiting_on_customer | waiting_on_agent | resolved | closed
    'priority'             => 'medium',            // low | medium | high | urgent
    'requester_source_id'  => '222',               // contacts source_id
    'assignee_source_id'   => '12345',             // agents source_id
    'department_source_id' => '111',               // departments source_id
    'tag_source_ids'       => ['billing'],         // array of tags source_ids
    'metadata'             => [],                  // arbitrary key/value preserved as-is
    'created_at'           => '2024-01-15T10:00:00Z',
    'updated_at'           => '2024-01-16T08:30:00Z',
]
```

### replies

```php
[
    'source_id'        => '444',
    'ticket_source_id' => '333',    // tickets source_id
    'body'             => '<p>Hello, please reset your password.</p>',
    'is_internal_note' => false,    // true for private/internal notes
    'author_source_id' => '12345',  // agents source_id (null if written by a contact)
    'created_at'       => '2024-01-15T10:05:00Z',
    'updated_at'       => '2024-01-15T10:05:00Z',
]
```

### attachments

```php
[
    'source_id'        => '555',
    'parent_type'      => 'reply',     // 'ticket' or 'reply'
    'parent_source_id' => '444',       // the source_id of the parent ticket or reply
    'filename'         => 'screenshot.png',
    'mime_type'        => 'image/png',
    'size'             => 204800,      // bytes
    'download_url'     => 'https://...',
]
```

The framework downloads and stores attachments using the `download_url`. If the URL is a temporary signed URL, ensure your adapter fetches attachments while the URL is still valid, or implement re-fetch logic in your extraction loop.
