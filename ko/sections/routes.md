# 라우트

Escalated는 설정된 접두사(기본값: `/support`) 아래에 세 그룹의 라우트를 등록합니다.

## 고객 라우트

| 메서드 | URL | 설명 |
| ------ | --- | ----------- |
| GET | /support | 고객 티켓 목록 |
| GET | /support/create | 새 티켓 양식 |
| POST | /support | 티켓 생성 |
| GET | /support/kb | 지식 베이스 홈 |
| GET | /support/kb/{slug} | 지식 베이스 문서 |
| POST | /support/kb/{slug}/feedback | 문서 피드백 |
| GET | /support/{reference} | 티켓 상세 |
| POST | /support/{reference}/reply | 티켓에 답변 |
| POST | /support/{reference}/close | 티켓 종료 |
| POST | /support/{reference}/reopen | 티켓 재오픈 |
| POST | /support/{reference}/rate | 만족도 평가 제출 |

## 에이전트 라우트

`escalated-agent` 게이트가 필요합니다.

| 메서드 | URL | 설명 |
| ------ | --- | ----------- |
| GET | /support/agent | 에이전트 대시보드 |
| GET | /support/agent/tickets | 티켓 큐 |
| GET | /support/agent/tickets/{reference} | 티켓 상세 |
| POST | /support/agent/tickets/{reference}/reply | 공개 답변 |
| POST | /support/agent/tickets/{reference}/note | 내부 메모 |
| POST | /support/agent/tickets/{reference}/assign | 에이전트 할당 |
| POST | /support/agent/tickets/{reference}/status | 상태 변경 |
| POST | /support/agent/tickets/{reference}/priority | 우선순위 변경 |
| POST | /support/agent/tickets/bulk | 티켓 일괄 작업 |
| POST | /support/agent/tickets/{reference}/follow | 팔로우 전환 |
| POST | /support/agent/tickets/{reference}/macro | 매크로 적용 |
| POST | /support/agent/tickets/{reference}/presence | 프레젠스 보고 |
| POST | /support/agent/tickets/{reference}/typing | 입력 상태 보고 |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | 메모 고정 전환 |

## 관리자 라우트

`escalated-admin` 게이트가 필요합니다. 관리자는 모든 에이전트 라우트와 관리 페이지에 접근할 수 있습니다.

| 메서드 | URL | 설명 |
| ------ | --- | ----------- |
| GET | /support/admin/reports | 분석 대시보드 |
| GET | /support/admin/departments | 부서 관리 |
| GET | /support/admin/sla-policies | SLA 정책 관리 |
| GET | /support/admin/escalation-rules | 에스컬레이션 규칙 빌더 |
| GET | /support/admin/tags | 태그 관리 |
| GET | /support/admin/canned-responses | 정형 응답 템플릿 |
| GET | /support/admin/macros | 매크로 관리 |
| GET | /support/admin/custom-fields | 커스텀 필드 및 양식 |
| GET | /support/admin/statuses | 커스텀 상태 |
| GET | /support/admin/business-hours | 영업시간 스케줄 |
| GET | /support/admin/roles | 에이전트 역할 및 권한 |
| GET | /support/admin/audit-log | 감사 추적 |
| GET | /support/admin/skills | 스킬 관리 |
| GET | /support/admin/capacity | 에이전트 용량 관리 |
| GET | /support/admin/automations | 시간 기반 자동화 |
| GET | /support/admin/webhooks | 아웃바운드 Webhook |
| GET | /support/admin/webhooks/{webhook}/deliveries | Webhook 전송 로그 |
| GET | /support/admin/kb-articles | 지식 베이스 문서 |
| GET | /support/admin/kb-categories | 지식 베이스 카테고리 |
| GET | /support/admin/reports/dashboard | 보고서 대시보드 |
| GET | /support/admin/reports/agents | 에이전트 생산성 보고서 |
| GET | /support/admin/reports/sla | SLA 달성 보고서 |
| GET | /support/admin/reports/csat | CSAT 보고서 |
| GET | /support/admin/settings/csat | CSAT 설문 설정 |
| GET | /support/admin/settings/sso | SSO 설정 |
| GET | /support/admin/settings/two-factor | 이중 인증 설정 |
| GET | /support/admin/settings/data-retention | 데이터 보존 설정 |
| GET | /support/admin/settings/email | 이메일 채널 설정 |
| GET | /support/admin/custom-objects | 커스텀 객체 |
| GET | /support/admin/custom-objects/{customObject}/records | 커스텀 객체 레코드 |
| GET | /support/admin/tickets/merge-search | 병합 대상 검색 |
| POST | /support/admin/tickets/{reference}/merge | 티켓을 대상에 병합 |
| GET | /support/admin/tickets/{reference}/links | 연결된 티켓 목록 |
| POST | /support/admin/tickets/{reference}/links | 관련 티켓 연결 |
| DELETE | /support/admin/tickets/{reference}/links/{link} | 관련 티켓 연결 해제 |
| GET | /support/admin/tickets/{reference}/side-conversations | 사이드 대화 목록 |
| POST | /support/admin/tickets/{reference}/side-conversations | 사이드 대화 시작 |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | 사이드 대화에 답변 |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | 사이드 대화 종료 |
| POST | /support/admin/macros | 매크로 생성 |
| PUT | /support/admin/macros/{macro} | 매크로 업데이트 |
| DELETE | /support/admin/macros/{macro} | 매크로 삭제 |

## 게스트 라우트

인증이 필요하지 않습니다. 고유한 토큰으로 접근합니다.

| 메서드 | URL | 설명 |
| ------ | --- | ----------- |
| GET | /support/guest/create | 게스트 티켓 양식 |
| POST | /support/guest | 게스트 티켓 생성 |
| GET | /support/guest/{token} | 게스트 티켓 보기 |
| POST | /support/guest/{token}/reply | 게스트 티켓에 답변 |
| POST | /support/guest/{token}/rate | 만족도 평가 제출 |
