# 配列、文字列

## 配列
MCScriptでは、基本的に配列の使用は非推奨です。基本的にはリストを使用し、配列が必要な時のみリストから変換するようにしてください。MCScriptで配列を使うメリットはほぼありません。

#### 配列の生成
配列の生成にはArray関数を使います。各要素は、Javaのデフォルト値[^1]で初期化されます。
```
array = Array(int, 10)
```
リストを配列に変換する場合は、第二引数にリストを渡します。
```
list = [1, 2, 3]
array = Array(int, list)
```
データを変換したい場合は、第三引数に関数を渡します。
```
list = ["abcd", "efg", "hi"]
array = Array(int, list, fun(s): s.length)
array # [4, 3, 2]
```
#### 要素にアクセス
MCScriptの要素へのアクセスは、負の値を指定出来ること以外Javaと変わりません。
```
array = Array(int, [1, 2, 3])
array[0] = 0
array[-1] = 4
array # [0, 2, 4]
```
#### 配列の長さを取得
配列の長さを取得するには、Length関数を使います。
```
array = Array(int, [1, 2, 3])
Length(array) # 3
```
## 文字列操作
MCScriptは、文字列をイミュータブルな文字の配列として扱えます。
```
str = "hello"
str[0] # h
str[-1] # o
```
また、リストのように指定範囲を切り出すことも出来ます。
```
str = "hello"
str[1:4] # ell
str[3:] # lo
str[:2] # he
str[:] # hello
```
[^1]: 基本数値型は0、charは'\u0000'、booleanはfalse、参照型はnullで初期化します。