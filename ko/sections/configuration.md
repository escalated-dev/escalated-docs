# 설정

Escalated는 적절한 기본값으로 즉시 사용할 수 있습니다. 설정은 선택사항이지만 커스터마이징이 가능합니다.

> **설정 옵션**
>
> - `routes.prefix` -- 모든 Escalated 라우트의 URL 접두사 (기본값: `support`)
> - `routes.middleware` -- 고객 라우트에 적용되는 미들웨어 (기본값: `['web', 'auth']`)
> - `user_model` -- 사용자 모델 클래스 (기본값: `App\Models\User`)
> - `table_prefix` -- 데이터베이스 테이블 접두사 (기본값: `escalated_`)
> - `tickets.allow_customer_close` -- 고객이 자신의 티켓을 종료할 수 있는지 여부 (기본값: `true`)
> - `tickets.auto_close_resolved_after_days` -- 해결된 티켓을 N일 후 자동 종료 (기본값: `7`)
> - `sla.business_hours_only` -- SLA 목표에 영업시간만 계산 (기본값: `false`)
> - `notifications.channels` -- 알림 채널 (기본값: `['mail', 'database']`)

## 관리 설정 및 모듈

최근 플랫폼 업데이트에서 다음의 설정 및 관리 화면이 추가되었습니다:

- 조건부 표시 규칙이 있는 커스텀 필드
- 커스텀 상태 및 영업시간 스케줄
- 역할(RBAC), 스킬 기반 라우팅, 에이전트 용량
- 감사 로그 검토
- 자동화 및 아웃바운드 Webhook
- CSAT 설문 동작
- SSO 및 이중 인증
- 데이터 보존 정책 및 퍼지 동작
- 이메일 채널 설정
- 커스텀 객체 및 레코드

## 에셋 퍼블리싱

```bash
# 설정 파일 퍼블리싱
$ php artisan vendor:publish --tag=escalated-config

# 커스터마이징을 위한 이메일 템플릿 퍼블리싱
$ php artisan vendor:publish --tag=escalated-views

# 마이그레이션 퍼블리싱 (커스터마이징이 필요한 경우)
$ php artisan vendor:publish --tag=escalated-migrations
```
