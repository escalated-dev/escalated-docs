イベントは`ActiveSupport::Notifications`経由でディスパッチされます。`ActiveSupport::Notifications.subscribe("escalated.ticket_created")`でサブスクライブしてください。
