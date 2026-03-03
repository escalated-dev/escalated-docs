## 1. パッケージのインストール

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Escalatedインストーラーの実行

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Filamentプラグインの登録

Filamentパネルプロバイダーに以下を追加します：

```php
use Escalated\Filament\EscalatedFilamentPlugin;

public function panel(Panel $panel): Panel
{
    return $panel
        ->plugin(
            EscalatedFilamentPlugin::make()
                ->navigationGroup('Support')
                ->agentGate('escalated-agent')
                ->adminGate('escalated-admin')
        );
}
```

> **注意：** FilamentはネイティブのLivewire + Bladeコンポーネントを使用するため、Inertia.jsやVueは不要です。UIはFilamentのデザインシステムに準拠しています。コア機能はInertiaフロントエンドと同じですが、一部の操作は若干異なる場合があります。
