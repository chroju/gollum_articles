snmpで任意の値を出力する
====

snmpd.confで`extend`もしくは`exec`ディレクティブを指定すると、任意のコマンド実行結果をextend MIBに出力できる。二者の相違点としては、`extend`は文字列OIDの固定が可能。

```
extend name command args
```

* 取得はNET-SNMP-EXTEND-MIB::nsExtendObjectsに対して実施する。
* 出力はSTRINGに限定されるため、INTEGERが欲しい場合は終了コードを活用する。ただし、終了コードは255までであるため、限界がある。

参考
----

* [19.6.5. Net-SNMP の拡張](https://access.redhat.com/documentation/ja-JP/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sect-System_Monitoring_Tools-Net-SNMP-Extending.html)
* [Umbrella　snmpdに外部コマンドを追加してHDD温度を取得する](http://wbbwbb.blog83.fc2.com/blog-entry-148.html)