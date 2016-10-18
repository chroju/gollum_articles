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
* `context` : Lambda関数のランタイム情報（実行関数名、ARN、実行残り時間等）。戻り値もここに指定する。
  * `context.succeed(Object result)` : 実行結果が成功とする。渡したJSONはログストリームに吐かれ、同期型の場合レスポンスボディにも入る。
  * `context.fail(Object result)` : 実行結果がエラーとする。渡したJSONはレスポンスヘッダにも入る。
  * `context.done(String message, Object result)` : `message`が指定されている場合のみエラーと判断される。

Invocationtype（実行タイプ）
----

2種類存在する。基本的には呼び出し方で決まるが、CLIから手動で`invoke`する場合はタイプを指定できる。

* `event` : 非同期。実行の正否のみを返す。
* `requestresponse` : 同期。`context.succeed`にセットされた値が返る。

API Gateway
----

API Gatewayからの実行を設定できる。メソッドを選択し、IAMによるアクセス制御を行うことが可能。Lambdaからの設定後、API Gateway上でDeployすることで使用可能になる。

tips
----

### 時刻の使用

実行環境のコンテナが複数回使い回されることがあるため、`handler`メソッド外で時刻を取得して変数に代入した場合、次回実行時も時刻が変わらないことがある。時刻の取得は`handler`の中で行うのがベター。 **基本的にhandlerの外で関数の実行は行わない（次回実行時に初期化が保証されない）**

* [AWS Lambda上でサーバ時刻がよくわからないことになって困った話 - Qiita](http://qiita.com/yutaro1985/items/a24b572624281ebaa0dd)
