# イベント、コマンド、スケジューリング
プラグインを開発する上で、イベントハンドラーの登録、コマンドの実装、処理のスケジューリングは必須です。
MCScriptでは、専用の構文を使って上記処理を簡潔に記述出来ます。

## イベント
イベントハンドラーの登録は、非常に簡単です。
@のマークの後にEvent名を記述し（Eventは省略）、ブロック内に処理を記述するだけです。
ブロック内では、event定数にイベントオブジェクトが渡されます。
```
@PlayerInteract {
    event.player.sendMessage("interact")
}
```
EventPriorityを指定する場合は、イベント名の後に括弧で記述します。
```
@PlayerInteract(LOWEST) {
    event.player.sendMessage("lowest")
}
```
## コマンド
コマンドの実装は、ほぼ関数宣言と同じです。
関数名をコマンド名として記述し、引数にその後に続く文字列が代入されます。
コマンド実行時、引数の数が一致している場合のみ実行されます。
関数内では、sender定数にCommandSenderが渡されます。
```
command test(arg1, arg2) {
    sender.sendMessage(arg1 + ":" + arg2)
}
```
minecraft
```
/test arg1 arg2 # arg1:arg2
/test arg1 # nothing
```
関数同様に、デフォルト引数が利用できます。
```
command test(arg1, arg2: "arg2") {
    sender.sendMessage(arg1 + ":" + arg2)
}
```
```
/test arg1 arg2 # arg1:arg2
/test arg1 # arg1:arg2
```
コマンドの引数を配列として受け取りたい場合、~を関数名の前につけます。
この場合、引数の数にかかわらず常に実行されます。
```
command ~test(args) {
    for (arg in args) {
        sender.sendMessage(arg)
    }
}
```
```
/test 1 2 3 4 5
/*
1
2
3
4
5
*/
```
## スケジューリング
MCScriptで処理をスケジューリングする場合、runnable式を使います。
```
r = runnable {
    Println("test")
}

r.run() # runTask(PLUGIN)
r.run(5) # runTaskLater(PLUGIN, 5)
r.run(0, 1) # runTaskTimer(PLUGIN, 0, 1)
```
runnable式では、最大実行回数を指定できます。
```
runnable(5) {
    Println(getCount())
}.run(0, 1)
/*
5
4
3
2
1
*/
```
runnable式のブロック内では、以下のメソッドが利用できます。
* cancel()
* isCancelled()
* getTaskId()
* setCount(int)
* getCount()