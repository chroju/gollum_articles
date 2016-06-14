* キューサービス。SNS等から連携されたキューメッセージを保持。エンドポイント（URL等）へのアクセスに応じてsendする。
* メッセージは「少なくとも1回」配信される。重複の可能性はあるため、受信側で冪等性を保証する必要がある。
* メッセージの順序は保証されない。
* 一度のポーリングでの受信メッセージ数は10までの間で指定できる。ただし、指定数より少ないメッセージが受信されることもある。
* メッセージは受信されても自動では削除されない。受信時に渡される「受信ハンドル」を使ってメッセージの削除をリクエストする必要がある。
* メッセージの保存期間はデフォルト4日間、最大2週間。

### Visibility Timeout（可視性タイムアウト）

* 一度受信したメッセージの重複受信を避けるため、一定期間メッセージは不可視になる。
* 受信側はメッセージを取得後、可視性タイムアウトの期間中にメッセージを削除することが望まれる。

### ロングポーリング

SQSへポーリングした際にメッセージが空であっても、SQSがすぐに応答を返さず、タイムアウトになるまでメッセージの受信を待機する設定。これによりポーリング回数の削減が期待できる。

cli
----

メッセージ数の確認。なお「ApproximateNumberOfMessages」で不可視状態のメッセージ数が取得できる。

```bash
$ aws sqs get-queue-attributes --queue-url https://xxx --attribute-names ApproximateNumberOfMessages
{
    "Attributes": {
        "ApproximateNumberOfMessages": "3"
    }
}
```

メッセージの受信

```bash
$ aws sqs receive-message --queue-url https://xxx --max-number-of-messages 5
{
    "Messages": [
        {
            "Body": "....",
            "ReceiptHandle": "AQEBNB....",
            "MD5OfBody": "18d86e....",
            "MessageId": "915ee2...."
        }
    ]
}
```

メッセージの削除

```bash
$ aws sqs delete-message --queue-url https://xxx --receipt-handle xxx
```

参考
----

* [Amazon SQSを利用する前に抑えておくべき7つのポイント - Qiita](http://qiita.com/masarufuruya/items/f91080c63691a984f691)
* [[JAWS-UG CLI] SQS:#3 メッセージの受信 (処理側) - Qiita](http://qiita.com/tcsh/items/7781fe238df82fc030d2)