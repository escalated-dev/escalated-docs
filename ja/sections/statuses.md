# ステータスと優先度

Escalatedではチケットを状態マシンとして扱います。ステータス遷移は強制され、設定可能です。

## ステータス

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## 優先度

- Low
- Medium
- High
- Urgent
- Critical

遷移は`config/escalated.php`の`transitions`キーで設定可能です。

管理者は管理パネル（`/support/admin/statuses`）でカスタムステータスを作成・管理できます。
