# 演算子
MCScriptでは符号なし右シフト、インクリメント、デクリメントを除き、Javaの演算子をすべて利用できます。この節では、Javaには無い演算子や、動作の違う演算子について解説します。
#### 整数除算演算子「//」
通常の除算を行った後に、小数点以下を切り捨てます。
```
Println(5d // 2) # 2
Println(1.5 // 1) # 1
```
#### べき乗演算子「**」
べき乗を計算します
```
Println(2 ** 8) # 256
Println(0 ** 0) # 1
```
//=、**=も利用出来ます。
#### 同値演算子「==」「!=」
同値演算子は、Javaのequalsメソッドにあたります。
```
Println("aaa" == String("aaa")) # true
Println("aaa" != String("aaa")) # false
```
#### 同一演算子「is」「isnot」
同一演算子は、Javaの「==」にあたります。
MCScriptの数値は、すべてラッパークラスで扱われるため、同一演算子での比較はできません。[^1]
```
Println(128 is 128) # false
Println(1d is 1d) # false
Println('a' is 'a') # false

a = null
Println(a is null) # true
Println(a isnot null) # false

a = true
Println(a is true) # true
```
#### 所属検査演算子「in」「notin」
右辺がコレクションの場合contains、Mapの場合containsKeyと同義です。配列の場合は各要素をループし、equalsメソッドで比較します。
```
list = [1, 2, 3]
Println(1 in list) # true
Println(1 notin list) # false

map = {"a":1, "b":2}
Println("a" in map) # true
Println(1 in map) # false

array = Array(int, 5)
array[3] = 1
Println(1 in array) # true
```
数値が範囲内かどうかを判定することも出来ます。
```
Println(4 in 1..10) # true
Println(4 notin 5..1) # false
```
#### Null合体演算子「?:」
左辺がnullであれば右辺を評価し、それ以外の場合左辺を評価します。
```
a = 1
Println(a ?: 2) # 1
a = null
Println(a ?: 2) # 2
```

[^1]: Javaでは-128から127までの整数を同一オブジェクトとして扱うため、その範囲であれば同一演算子で比較可能です。