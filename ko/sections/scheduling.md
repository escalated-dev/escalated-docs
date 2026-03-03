# 스케줄링

Escalated는 자동화된 티켓 라이프사이클 관리를 위한 artisan 명령을 제공합니다. 스케줄러에 추가하세요.

```php
use Illuminate\Support\Facades\Schedule;

// SLA 위반 확인
Schedule::command('escalated:check-sla')->everyMinute();

// 에스컬레이션 규칙 평가
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// 시간 기반 자동화 실행
Schedule::command('escalated:run-automations')->everyFiveMinutes();

// 설정된 일수 후 해결된 티켓 자동 종료
Schedule::command('escalated:close-resolved')->daily();

// 오래된 활동 로그 항목 퍼지
Schedule::command('escalated:purge-activities')->weekly();

// 보존 설정에 따른 데이터 퍼지
Schedule::command('escalated:purge-expired')->daily();

// 인바운드 IMAP 메일박스 폴링 (IMAP 인바운드 어댑터 사용 시만)
Schedule::command('escalated:poll-imap')->everyMinute();
```

## 사용 가능한 명령

- `escalated:check-sla` -- 오픈 티켓을 SLA 정책과 대조하고 `SlaBreached` 이벤트를 디스패치
- `escalated:evaluate-escalations` -- 일치하는 티켓에 대해 에스컬레이션 규칙을 실행하고 설정된 작업을 적용
- `escalated:run-automations` -- 대상 티켓에 대해 시간 기반 자동화 규칙을 실행
- `escalated:close-resolved` -- 설정된 일수 동안 "resolved" 상태였던 티켓을 종료
- `escalated:purge-activities` -- 설정된 보존 기간보다 오래된 활동 로그 항목을 삭제
- `escalated:purge-expired` -- 보존 정책 설정에 따라 티켓, 첨부 파일, 감사 로그를 퍼지
- `escalated:poll-imap` -- 설정된 IMAP 메일박스를 폴링하여 인바운드 이메일 답변을 가져옴
