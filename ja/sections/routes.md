# ルート

Escalatedは設定されたプレフィックス（デフォルト：`/support`）の下に3つのルートグループを登録します。

## カスタマールート

| メソッド | URL | 説明 |
| ------ | --- | ----------- |
| GET | /support | カスタマーチケット一覧 |
| GET | /support/create | 新規チケットフォーム |
| POST | /support | チケット作成 |
| GET | /support/kb | ナレッジベースホーム |
| GET | /support/kb/{slug} | ナレッジベース記事 |
| POST | /support/kb/{slug}/feedback | 記事フィードバック |
| GET | /support/{reference} | チケット詳細 |
| POST | /support/{reference}/reply | チケットへの返信 |
| POST | /support/{reference}/close | チケットのクローズ |
| POST | /support/{reference}/reopen | チケットの再オープン |
| POST | /support/{reference}/rate | 満足度評価の送信 |

## エージェントルート

`escalated-agent`ゲートが必要です。

| メソッド | URL | 説明 |
| ------ | --- | ----------- |
| GET | /support/agent | エージェントダッシュボード |
| GET | /support/agent/tickets | チケットキュー |
| GET | /support/agent/tickets/{reference} | チケット詳細 |
| POST | /support/agent/tickets/{reference}/reply | 公開返信 |
| POST | /support/agent/tickets/{reference}/note | 内部メモ |
| POST | /support/agent/tickets/{reference}/assign | エージェントの割り当て |
| POST | /support/agent/tickets/{reference}/status | ステータスの変更 |
| POST | /support/agent/tickets/{reference}/priority | 優先度の変更 |
| POST | /support/agent/tickets/bulk | チケット一括操作 |
| POST | /support/agent/tickets/{reference}/follow | フォローの切り替え |
| POST | /support/agent/tickets/{reference}/macro | マクロの適用 |
| POST | /support/agent/tickets/{reference}/presence | プレゼンスの報告 |
| POST | /support/agent/tickets/{reference}/typing | 入力状態の報告 |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | メモのピン留めの切り替え |

## 管理者ルート

`escalated-admin`ゲートが必要です。管理者はすべてのエージェントルートに加えて管理ページにアクセスできます。

| メソッド | URL | 説明 |
| ------ | --- | ----------- |
| GET | /support/admin/reports | 分析ダッシュボード |
| GET | /support/admin/departments | 部門管理 |
| GET | /support/admin/sla-policies | SLAポリシー管理 |
| GET | /support/admin/escalation-rules | エスカレーションルールビルダー |
| GET | /support/admin/tags | タグ管理 |
| GET | /support/admin/canned-responses | 定型返信テンプレート |
| GET | /support/admin/macros | マクロ管理 |
| GET | /support/admin/custom-fields | カスタムフィールドとフォーム |
| GET | /support/admin/statuses | カスタムステータス |
| GET | /support/admin/business-hours | 営業時間スケジュール |
| GET | /support/admin/roles | エージェントのロールと権限 |
| GET | /support/admin/audit-log | 監査証跡 |
| GET | /support/admin/skills | スキル管理 |
| GET | /support/admin/capacity | エージェントキャパシティ管理 |
| GET | /support/admin/automations | 時間ベースの自動化 |
| GET | /support/admin/webhooks | 送信Webhook |
| GET | /support/admin/webhooks/{webhook}/deliveries | Webhook配信ログ |
| GET | /support/admin/kb-articles | ナレッジベース記事 |
| GET | /support/admin/kb-categories | ナレッジベースカテゴリ |
| GET | /support/admin/reports/dashboard | レポートダッシュボード |
| GET | /support/admin/reports/agents | エージェント生産性レポート |
| GET | /support/admin/reports/sla | SLA達成レポート |
| GET | /support/admin/reports/csat | CSATレポート |
| GET | /support/admin/settings/csat | CSAT調査設定 |
| GET | /support/admin/settings/sso | SSO設定 |
| GET | /support/admin/settings/two-factor | 二要素認証設定 |
| GET | /support/admin/settings/data-retention | データ保持設定 |
| GET | /support/admin/settings/email | メールチャネル設定 |
| GET | /support/admin/custom-objects | カスタムオブジェクト |
| GET | /support/admin/custom-objects/{customObject}/records | カスタムオブジェクトレコード |
| GET | /support/admin/tickets/merge-search | マージ対象の検索 |
| POST | /support/admin/tickets/{reference}/merge | チケットを対象にマージ |
| GET | /support/admin/tickets/{reference}/links | リンク済みチケット一覧 |
| POST | /support/admin/tickets/{reference}/links | 関連チケットのリンク |
| DELETE | /support/admin/tickets/{reference}/links/{link} | 関連チケットのリンク解除 |
| GET | /support/admin/tickets/{reference}/side-conversations | サイドカンバセーション一覧 |
| POST | /support/admin/tickets/{reference}/side-conversations | サイドカンバセーションの開始 |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | サイドカンバセーションへの返信 |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | サイドカンバセーションのクローズ |
| POST | /support/admin/macros | マクロの作成 |
| PUT | /support/admin/macros/{macro} | マクロの更新 |
| DELETE | /support/admin/macros/{macro} | マクロの削除 |

## ゲストルート

認証不要。一意のトークンでアクセスします。

| メソッド | URL | 説明 |
| ------ | --- | ----------- |
| GET | /support/guest/create | ゲストチケットフォーム |
| POST | /support/guest | ゲストチケットの作成 |
| GET | /support/guest/{token} | ゲストチケットの表示 |
| POST | /support/guest/{token}/reply | ゲストチケットへの返信 |
| POST | /support/guest/{token}/rate | 満足度評価の送信 |
