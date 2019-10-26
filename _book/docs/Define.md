# Define
MCScriptでは、YAMLを編集することで、Cのdefineに近い処理が可能です。
config.ymlと同じ位置にあるdefine.ymlに定義を記述していきます。
```yaml
CON: "CONSTANT"
```
キーと値を定義することによって、実行前にスクリプト内のキーに一致する文字列が置換されます。
```
Println("CON") # CONSTANT
```
あくまでスクリプトの一致部分のみを書き換えるため、ダブルクォーテーションで括る必要があります。
定数のように扱いたい場合は、以下のようにします。
```yaml
CON: "\"CONSTANT\""
```
```
Println(CON) # CONSTANT
```
また、引数を受け取って文字列に埋め込むことも出来ます。
```
INCREMENT(A): "A += 1"
CONCAT(S1, S2): "\"S1 S2\""
```
```
i = 0
Println(INCREMENT(i)) # 1
Println(CONCAT(hello, world)) # hello world
```
引数の左右のスペースは無視されます。
```
Println(CONCAT( This is , my book.  )) # this is my book.
```