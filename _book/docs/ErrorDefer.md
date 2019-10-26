# エラー処理、遅延実行

## エラー処理
MCScriptでは、スクリプト内部のエラーとJavaの例外をScriptErrorとしてまとめて扱います。
```
1 / 0 # line:1 / by zero
```
```
Integer.parseInt("a") # line:1 java.lang.NumberFormatException: For input string: "a"
```

### throw
意図的にエラーを発生させたい場合は、throw文を使います。
```
throw "error"
```
ScriptErrorは、行番号とエラーメッセージ以外の情報を持ちません。

### try-catch
Java同様に投げられたエラーをtry-catchを使って処理できます。
```
fun err() {
    throw "error"
}

try {
    err()
} catch e {
    e.print()
}
```
この場合、eにScriptErrorをラップしたErrorObjectが渡されます。
ErrorObjectには、lineNumber、messageプロパティに加え、内容を出力するprintメソッドが実装されています。
## 遅延実行
defer文を使って処理を事前に登録しておき、最後にLIFOで実行することができます。
```
defer Println("third")
Println("first")
defer Println("second")
/*
first
second
third
*/
```
defer文を関数内に記述すると、その関数を抜ける際に処理されます。
```
fun print() {
    defer Println("second")
    Println("first")
}

print()
defer Println("third")
/*
first
second
third
*/
```
エラーによって中断された場合でも処理を実行します。
```
fun err() {
    defer Println("first")
    throw "error"
}

try {
    defer Println("third")
    throw "error"
} catch e {
    defer Println("second")
    err()
}
/*
first
second
third
line:3 error
*/
```
defer文を呼び出した時点で、最後に実行されるべき処理を記述します。
```
import java.io.FileInputStream;
import java.io.FileOutputStream;

fun copy(from, to) {
    try {
        input = FileInputStream(from)
        defer input.close()

        output = FileOutputStream(to)
        defer output.close()

        while (c = input.read()) != -1 {
            output.write(c)
        }

        output.flush()
    } catch e {
        e.print()
    }
}
```