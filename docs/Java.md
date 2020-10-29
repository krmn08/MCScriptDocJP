# Java
MCScriptはJava上で動作しているスクリプト言語です。MCScriptのあらゆるオブジェクトは、Javaのオブジェクトでもあります。
そして、MCScriptではJavaのオブジェクトをJavaと同じ感覚で扱えます。メソッド呼び出しや、フィールドアクセスなど、Javaと構文は変わりません。

この節では、基本的なJavaの構文に加えて、MCScriptで独自に実装されている機能について解説します。
## インポート
Javaと同様に、import文でクラスをインポートできます。
```
import java.util.Calendar
```
上記では、Calender定数にClassObjectを代入しています。
```
const Calendar = java.util.Calendar
Calender # ClassObject class
Calender.class # Calendar class
```
また、ワイルドカードを使ったインポートもサポートしています。
```
import java.util.*
```
## オブジェクトの生成
Javaと違いオブジェクトの生成時にnewを付ける必要はありません。
```
vector = Vector(0, 0, 0)
```
## メソッド呼び出し
MCScriptでは、メソッド呼び出しの際、引数に型を指定することができます。
この場合、型が完全に一致していないと実行されません。
```java
void call(String pre, String s) {
    System.out.println(pre + "String");
}
void call(String pre, Object o) {
    System.out.println(pre + "Object");
}
```
```
call("class: ", "string": Object) # class: Object
```
また、引数に配列を展開して渡したい場合は、varargを使います。
```java
void call(int... args) {
    System.out.println(Arrays.toString(args));
}
void call(String str, int i) {
    System.out.println(str + i);
}
```
```
array = Array(int, 5);
for i in 0 until 5 {
    array[i] = i;
}
call(vararg array)

array = Array(Object, ["abc", 3])
call(vararg array)
```
## プロパティ
MCScriptには、プロパティという機能が実装されています。
プロパティとは、getter、setterを隠蔽する機能です。
フィールドにアクセスしているように見えますが、内部的にはgetter、setterが呼び出されています。
```
vector = Vector(0, 1, 2)
vector.x = 1
vector.y = vector.z
vector.z = 3
vector # Vector(1, 2, 3)
```
メソッド名の頭に、get、is、setのいずれかが付いていればプロパティ機能が利用可能です。
プロパティ名の先頭に続く大文字をすべて小文字に変換します。
```
player = getPlayer("PlayerName")
player.displayName # PlayerName
```
## Unsafe Access
メンバー名の後に`!`を付ける事で、本来アクセス不可能なメンバーにアクセス出来るようになります。
```java
class Test {
    private int i = 1;

    private Test() {}

    private void call() {
        Println("test");
    }
}
```
```
test = Test!()
Println(test.i!) # 1
Println(test.call!()) # test
```
フィールドにアクセスする場合、プロパティよりも高速に動作しますが、危険な操作のため注意して利用してください。
## 拡張関数
MCScriptでは、既存のクラスを拡張してメソッドを追加できます。
関数内部では、this定数にレシーバオブジェクトが渡されます。
```
fun String.count(ch) {
    count = 0
    for c in this.toCharArray() {
        if (c == ch) {
            count += 1
        }
    }
    count
}

"ababababa".count('a') # 5
```
拡張関数は、すべてのスコープから利用できます。
## 関数型インターフェース
MCScriptではクラスの定義ができないため、関数型インターフェースを実装することができません。その代わりに、引数の型が関数型インターフェースであれば、MCScriptの関数オブジェクトを関数型インターフェースに変換します。
```
list = ["abc", "defg", "hijkl"]
list.stream()\
        .map(s -> s.length())\
        .forEach(Println)
/*
3
4
5
*/
```
また、Javaのメソッドも同様に変換されます。
```
list = ["abc", "defg", "hijkl"]
list.stream()\
        .map(s -> s.toUpperCase())\
        .forEach(System.out.println)
/*
ABC
DEFG
HIJKL
*/
```