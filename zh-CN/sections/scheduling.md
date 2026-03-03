# 调度

Escalated提供了用于自动化工单生命周期管理的artisan命令。请将它们添加到您的调度器中。

```php
use Illuminate\Support\Facades\Schedule;

// 检查SLA违规
Schedule::command('escalated:check-sla')->everyMinute();

// 评估升级规则
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// 运行基于时间的自动化
Schedule::command('escalated:run-automations')->everyFiveMinutes();

// 配置天数后自动关闭已解决的工单
Schedule::command('escalated:close-resolved')->daily();

// 清理旧的活动日志条目
Schedule::command('escalated:purge-activities')->weekly();

// 根据保留设置清理数据
Schedule::command('escalated:purge-expired')->daily();

// 轮询入站IMAP邮箱（仅在使用IMAP入站适配器时）
Schedule::command('escalated:poll-imap')->everyMinute();
```

## 可用命令

- `escalated:check-sla` -- 检查未关闭工单是否符合SLA策略，并触发`SlaBreached`事件
- `escalated:evaluate-escalations` -- 对匹配的工单运行升级规则并应用配置的操作
- `escalated:run-automations` -- 对符合条件的工单运行基于时间的自动化规则
- `escalated:close-resolved` -- 关闭处于"resolved"状态达到配置天数的工单
- `escalated:purge-activities` -- 删除超过配置保留期的活动日志条目
- `escalated:purge-expired` -- 根据保留策略设置清理工单、附件和审计日志
- `escalated:poll-imap` -- 轮询配置的IMAP邮箱以获取入站邮件回复
