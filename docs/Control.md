# 制御文
MCScriptの制御文は、Javaの制御文をほぼ引き継いでいますが、以下の制限があります。
* if文の中括弧を省略できない
* ラベルが無いため、複数のループを抜けられない

上記機能を実装しなかったのは、無くても困らない上、ソースの可読性を下げる可能性があるからです。

しかし、MCScriptではifやswitchを式として扱えたり、拡張forが更に強化されるなど、利便性が向上しています。この節では、そのような制御文について詳しく解説していきます。
## 条件分岐
MCScriptの条件分岐には、Javaとの大きな差異はありません。
#### if
MCScriptのifは括弧を省略可能です。
```
x = 1
if x == 1 {
    do()
}
```
else ifの代わりにelifを使います。
```
x = 1
if x < 0 {
    do1()
} elif x > 0 {
    do2()
} else {
    do3()
}
```
また、式としても扱えます。[^1]
```
x = 1
abs = if x < 0 { -x } else { x }
```
#### switch
MCScriptのswitchは、Java12で実装されたSwitchExpressionに近似しています。
```
str = "one"
num = switch str {
    "one" -> 1
    "two" -> {
        2
    }
    default -> 0
}
```
複数のケースをまとめる場合、括弧で括る必要があります。
```
day = "Sunday"
switch day {
    ("Saturday", "Sunday") -> Println("It's a holiday");
    default -> Println("It's a weekday");
}
```
そして、Javaとの最も大きな違いは、型に制限がない事です。MCScriptでは、すべてのケースをequalsで比較し、実行します。
```
class = int
switch class {
    String -> Println("It's a String");
    int -> Println("It's a int");
    boolean -> Println("It's a boolean");
    default -> Println("Don't know type: " + class);
}
```
## 繰り返し
MCScriptのforやwhileはJavaと同じ役割を担いますが、括弧を省略するなど構文に一部変更があります。
#### for
従来の形でfor文を記述できます。
MCScriptではパフォーマンスや可読性などの面から、基本的に下で紹介するRangeObjectの利用を推奨します。
```
for i = 0; i < 10; i += 1 {
    Println(i)
}
```
#### for-each
for-eachでは、コロンの代わりにinを使います。
```
list = [1, 2, 3]
for i in list {
    Println(i)
}
```
変数を二つ記述することで、インデックスを取得できます。
```
list = ["a", "b", "c"]
for i, str in list {
    Println(i + ": " + str)
}
```
マップもfor-eachで処理可能です。
```
map = { 1:"a", 2:"b" }
for k, v in map {
    Println(k + ":" + v)
}
```
変数が一つの場合はキーが代入されます。
#### RangeObject
MCScriptでは、数値をドット二つで繋ぐことでRangeObjectを生成します。
RangeObjectは、整数のIterableとして動作します。
```
for i in 0..3 {
    Println(i)
}
/*
0
1
2
3
*/

for i in -3..0 {
    Println(i)
}
/*
-3
-2
-1
0
*/
```
untilで終値を含まないRangeObjectを生成します。
```
for i in 0 until 3 {
    Println(i)
}
/*
0
1
2
*/
for i in -3 until 0 {
    Println(i)
}
/*
-3
-2
-1
*/
```
stepで変化量を指定できます。
```
for i in 0..10 step 3 {
    Println(i)
}
/*
0
3
6
9
*/

for i in 10..0 step 3 {
    Println(i)
}
/*
10
7
4
1
*/
```
#### while
whileの動作に変更はありませんが、無限ループの記述を省略することができます。
```
while {
    # infinite loop
}
```
[^1]: 単純な処理では、条件演算子を使うと簡潔に記述できます。