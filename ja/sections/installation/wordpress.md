## 1. プラグインのインストール

```bash
$ wp plugin install escalated --activate
```

## 2. 設定

wp-adminの**Escalated -> Settings**に移動して、部門、SLAポリシー、エスカレーションルール、メールチャネルを設定します。

## 3. ショートコードの追加

任意のページにショートコードを配置して、顧客にサポートポータルを提供します：

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **注意：** WordPressプラグインは自己完結型で、Inertia.jsを使用しません。すべてのUIはネイティブのWordPress管理画面とショートコードベースのフロントエンドテンプレートで描画されます。
