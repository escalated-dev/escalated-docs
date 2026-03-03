## 1. 플러그인 설치

```bash
$ wp plugin install escalated --activate
```

## 2. 설정

wp-admin에서 **Escalated -> Settings**로 이동하여 부서, SLA 정책, 에스컬레이션 규칙, 이메일 채널을 설정합니다.

## 3. 쇼트코드 추가

아무 페이지에나 쇼트코드를 배치하여 고객에게 지원 포털을 제공합니다:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **참고:** WordPress 플러그인은 자체 완결형으로 Inertia.js를 사용하지 않습니다. 모든 UI는 네이티브 WordPress 관리 화면과 쇼트코드 기반 프론트엔드 템플릿으로 렌더링됩니다.
