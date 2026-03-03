## 1. 패키지 설치

```bash
$ composer require escalated-dev/escalated-laravel escalated-dev/escalated-filament
```

## 2. Escalated 인스톨러 실행

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. Filament 플러그인 등록

Filament 패널 프로바이더에 다음을 추가합니다:

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

> **참고:** Filament는 네이티브 Livewire + Blade 컴포넌트를 사용하므로 Inertia.js나 Vue가 필요하지 않습니다. UI는 Filament의 디자인 시스템을 따릅니다. 핵심 기능은 Inertia 프론트엔드와 동일하지만, 일부 인터랙션이 약간 다를 수 있습니다.
