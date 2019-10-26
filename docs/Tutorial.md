# チュートリアル

この章ではMCScriptの基本を解説します。

MCScriptの構文は、Javaをベースに最新の言語の要素を取り込んだものです。
一部プラグイン開発用の構文などが追加されていますが、基本的にJavaの構文を簡略化したものが多く、扱いは簡単です。

Javaでは文の最後にセミコロンが必要ですが、MCScriptでは行端に自動で挿入されるため不要です。
上記の仕様により、スクリプトのフォーマットに一部制限がかかる場合もあります。最低限可読性を下げないようにしていますが、Javaで出来る記述方法ができない場合もあるため、基本的にこのドキュメントのフォーマットに従ってください。

フォーマットの例
```
if condition
{
    # error
}

if condition {
    # pass
}

sb = StringBuilder()

# error
sb.append("a")
    .append("b")
    .append("c")

# pass
sb.append("a")\
    .append("b")\
    .append("c")

sb.append("a").
    append("b").
    append("c")

sb.append(
    "a"
).append(
    "b"
).append("c")

# error
a = "a"
    + "b"

# pass
a = "a" +
    "b"
```

予約語一覧
```
runnable    const       import      null        instanceof
is          isnot       in          notin       fun
command     true        false       while       for
break       continue    switch      default     if
elif        else        return      vararg      throw
try         catch       defer       boolean     char
byte        short       int         long        float
double
```