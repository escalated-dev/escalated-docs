# User Model

Your user model must implement the Ticketable contract so Escalated can associate tickets with users.

## User key types (UUID / string IDs)

Escalated stores references to your application's users (a ticket's requester
and assignee, a reply's author, an activity's causer, and so on). By default it
assumes your user **primary key is an integer**, which matches most apps.

If your users table uses a **UUID or other string primary key**, Escalated still
works — you just tell it the key type so the columns that store a user reference
are created to match. Integer-keyed apps need no change; everything below
defaults to the existing integer behavior, so this is a non-breaking, opt-in
setting.

| Framework | How to enable UUID / string user keys |
|-----------|----------------------------------------|
| **Laravel** / **Filament** | `ESCALATED_USER_KEY_TYPE` env (or `config/escalated.php` → `user_key_type`). Default `auto` detects the type from your `User` model's key (`int` → `bigint`, `HasUuids` → `uuid`, `HasUlids` → `ulid`); override with `bigint`/`uuid`/`ulid`/`string`. |
| **NestJS** | `ESCALATED_USER_KEY_TYPE` env: `int` (default), `bigint`, `uuid`, or `string`. Read at startup since TypeORM column types are fixed at load time. |
| **AdonisJS** | `ESCALATED_USER_KEY_TYPE` env: `int` (default), `bigint`, `uuid`, or `string`. Set it before running the Escalated migrations. |
| **Rails** | `config.user_id_type` in the initializer. Default `:auto` introspects your `user_class` primary key; override with `:bigint`/`:uuid`/`:string`. Re-run `escalated:install:migrations` after changing it. |
| **Symfony** | `ESCALATED_USER_KEY_TYPE` env: `int` (default), `bigint`, `uuid`, or `string`. Generate a Doctrine migration after changing it. |
| **Phoenix** | `config :escalated, user_key_type: :integer` (default), `:binary_id` (UUID), or `:string`. Compile-time config — recompile the dependency after changing it. |
| **Go** | `ESCALATED_USER_KEY_TYPE` env: `int` (default), `bigint`, `uuid`, or `string`. Host user IDs are exposed as the string-friendly `models.UserID` type. |
| **Django** | **Automatic** — references use `ForeignKey(AUTH_USER_MODEL)` / `CharField`, so any integer, UUID, or string user primary key works with no configuration. |
| **.NET** | **Automatic** — host user IDs are exchanged as `string` throughout, so integer, `Guid`, or string user keys all work. Your `IUserDirectory` implementation uses `string` IDs. |
| **Spring** | **Automatic** — the optional host-user link columns are stored as strings, so a UUID/string user key can be linked. |
| **WordPress** | Not applicable — WordPress user IDs are always integers. |

For UUID and string key types, user-reference columns are created as a portable
string column (for example `varchar(255)`) that holds a UUID or a stringified
integer ID. Existing integer-keyed installations are unaffected by the default.
