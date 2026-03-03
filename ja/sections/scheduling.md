# スケジューリング

Escalatedはチケットライフサイクルの自動管理用のartisanコマンドを提供しています。スケジューラーに追加してください。

```php
use Illuminate\Support\Facades\Schedule;

// SLA違反のチェック
Schedule::command('escalated:check-sla')->everyMinute();

// エスカレーションルールの評価
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// 時間ベースの自動化の実行
Schedule::command('escalated:run-automations')->everyFiveMinutes();

// 設定日数経過後の解決済みチケットの自動クローズ
Schedule::command('escalated:close-resolved')->daily();

// 古いアクティビティログエントリのパージ
Schedule::command('escalated:purge-activities')->weekly();

// 保持設定に基づくデータのパージ
Schedule::command('escalated:purge-expired')->daily();

// 受信IMAPメールボックスのポーリング（IMAP受信アダプター使用時のみ）
Schedule::command('escalated:poll-imap')->everyMinute();
```

## 利用可能なコマンド

- `escalated:check-sla` -- オープンチケットをSLAポリシーに照合し、`SlaBreached`イベントをディスパッチ
- `escalated:evaluate-escalations` -- 一致するチケットに対してエスカレーションルールを実行し、設定されたアクションを適用
- `escalated:run-automations` -- 対象のチケットに対して時間ベースの自動化ルールを実行
- `escalated:close-resolved` -- 設定された日数の間「resolved」ステータスであったチケットをクローズ
- `escalated:purge-activities` -- 設定された保持期間を超えたアクティビティログエントリを削除
- `escalated:purge-expired` -- 保持ポリシー設定に基づいてチケット、添付ファイル、監査ログをパージ
- `escalated:poll-imap` -- 設定されたIMAPメールボックスをポーリングして受信メール返信を取得
