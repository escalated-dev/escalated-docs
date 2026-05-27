## 1. 패키지 설치

```bash
$ composer require escalated-dev/escalated-laravel
```

## 2. 인스톨러 실행

마이그레이션, 설정을 퍼블리싱하고 데이터베이스 테이블을 설정합니다.

```bash
$ php artisan escalated:install
$ php artisan migrate
```

## 3. 설정 퍼블리싱 (선택)

```bash
$ php artisan vendor:publish --tag=escalated-config
```

> **참고:** 라우트는 서비스 프로바이더를 통해 자동으로 등록됩니다. `routes/web.php`에 추가할 필요가 없습니다.
