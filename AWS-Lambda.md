handler
----

Lambdaから呼び出す関数名はhandlerとして指定する。

```python
def handler_name(event, context): 
    ...
    return some_value
```

```js
exports.myHandler = function(event, context) {
   console.log("value1 = " + event.key1);
   console.log("value2 = " + event.key2);  
   context.succeed("some message");  
}
```

上記の関数を明示したpythonコードを`lambda_python.py`として保存した場合、Lambdaの実行対象handlerは`lambda_python.handler_name`となる。引数の内容は以下の通り。

* `event` : 実行元から渡されるイベントデータ。
* `context` : Lambda関数のランタイム情報（実行関数名、ARN、実行残り時間等）。
  `context.succeed`にセットした値は、requestResponce型の呼び出しにおいては戻り値になる。

API Gateway
----

API Gatewayからの実行を設定できる。メソッドを選択し、IAMによるアクセス制御を行うことが可能。Lambdaからの設定後、API Gateway上でDeployすることで使用可能になる。