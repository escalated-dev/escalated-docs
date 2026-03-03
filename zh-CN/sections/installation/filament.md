## 1. 安装包

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. 运行Escalated安装程序

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. 注册Filament插件

在Filament面板提供者中：

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

> **注意：** Filament使用原生Livewire + Blade组件——不需要Inertia.js或Vue。UI遵循Filament的设计系统。核心功能与Inertia前端相同，但某些交互可能略有不同。
