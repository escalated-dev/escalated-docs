# 상태 및 우선순위

Escalated는 티켓을 상태 머신으로 취급합니다. 상태 전환은 강제되며 설정 가능합니다.

## 상태

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## 우선순위

- Low
- Medium
- High
- Urgent
- Critical

전환은 `config/escalated.php`의 `transitions` 키에서 설정할 수 있습니다.

관리자는 관리 패널(`/support/admin/statuses`)에서 커스텀 상태를 생성하고 관리할 수 있습니다.
