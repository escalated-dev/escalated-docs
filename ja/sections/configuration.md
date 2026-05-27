# 設定

Escalatedは適切なデフォルト値でそのまま動作します。設定は任意ですが、カスタマイズも可能です。

> **設定オプション**
>
> - `routes.prefix` -- すべてのEscalatedルートのURLプレフィックス（デフォルト：`support`）
> - `routes.middleware` -- カスタマールートに適用されるミドルウェア（デフォルト：`['web', 'auth']`）
> - `user_model` -- ユーザーモデルクラス（デフォルト：`App\Models\User`）
> - `table_prefix` -- データベーステーブルのプレフィックス（デフォルト：`escalated_`）
> - `tickets.allow_customer_close` -- 顧客が自分のチケットをクローズできるかどうか（デフォルト：`true`）
> - `tickets.auto_close_resolved_after_days` -- 解決済みチケットをN日後に自動クローズ（デフォルト：`7`）
> - `sla.business_hours_only` -- SLA目標に営業時間のみをカウント（デフォルト：`false`）
> - `notifications.channels` -- 通知チャネル（デフォルト：`['mail', 'database']`）

## 管理設定とモジュール

最近のプラットフォームアップデートでは、以下の設定・管理画面が追加されました：

- 条件付き表示ルールを持つカスタムフィールド
- カスタムステータスと営業時間スケジュール
- ロール（RBAC）、スキルベースルーティング、エージェントキャパシティ
- 監査ログの確認
- 自動化と送信Webhook
- CSAT調査の動作設定
- SSOと二要素認証
- データ保持ポリシーとパージ動作
- メールチャネル設定
- カスタムオブジェクトとレコード

## アセットの公開

```bash
# 設定ファイルの公開
$ php artisan vendor:publish --tag=escalated-config

# カスタマイズ用のメールテンプレートの公開
$ php artisan vendor:publish --tag=escalated-views

# マイグレーションの公開（カスタマイズが必要な場合）
$ php artisan vendor:publish --tag=escalated-migrations
```
