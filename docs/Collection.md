# リスト、マップ、YAML
この節では、MCScriptのリスト、マップ、YAMLについて解説します。
## リスト
リストの作成には、リストリテラルを利用します。
```
list = [1, 2, 3]
list = [
    1,
    2,
    3
]
list = []
```
MCScriptのリストは、ArrayListで実装されています。Javaのようにメソッドを呼び出して操作することもできますが、MCScriptではより直感的に扱えます。
#### 要素にアクセス
Javaではgetまたはsetメソッドを使って要素にアクセスしますが、MCScriptではリストに対して、配列のようにアクセスすることができます。
また、添字に負の値を指定することで、後方からのインデックスを指定する事ができます。この動作は、配列、文字列の添字にも適用されます。
```
list = [1, 2, 3]
list[1] # 2
list[1] = 1
list # [1, 1, 3]
```
#### 要素を追加、削除
組み込み関数Add、Removeを使うことで効率よく処理できます。
```
list = ["abc", "def"]
Add(list, "ghi")
Remove(list, 1)
Remove(list, "abc")
list # ["ghi"]
```
#### リストを範囲選択
MCScriptでは、リストを添字で範囲選択することができます。内部的にJavaのsubListを利用しているため、元のリストへの参照が保持されます。
```
list = [1, 2, 3]
list[1:3] # [2, 3]
list[0:0] # []
```
また、添字を省略することもできます。
```
list = [1, 2, 3]
list[1:] # [2, 3]
list[:2] # [1, 2]
list[:] # [1, 2, 3]
```
#### リストの一部を削除
リストの範囲選択を利用して、選択範囲を削除することもできます。
```
list = [1, 2, 3]
list[1:].clear()
list # [1]
```
## マップ
マップの作成には、マップリテラルを利用します。
```
map = {1:"a", 2:"b", 3:"c"}
map = {
    1:"a",
    2:"b",
    3:"c"
}
map = {}
```
MCScriptのマップは、LinkedHashMapで実装されているため、挿入した順序を保持します。リスト同様、便利な構文がいくつか用意されています。
#### マップにアクセス
リストと同様に、添字でマップにアクセスすることができます。これは、Javaのget、putと同じ動作をします。
```
map = {1:"a", "2":"b", obj:"c"}
map[1] # a
map["2"] # b
map[obj] # c

map[obj] = "object"
```
また、キーが文字列の場合、ドットでもアクセス可能です。
```
map = {}
map.a = 1
map # {"a":1}
map.a # 1
```
## YAML
MCScriptでは、YamlConfigurationをマップのように扱うことができます。

plugins/MCScript/test.yml
```yml
a: 1
ab:
  cd:
    ef: "2"
list:
  - 1
  - 2
  - 3
n:
```
```
path = "plugins/MCScript/test.yml"
yaml = Load(path) # YamlConfiguration.load(new File(path))
yaml["a"] + 1 # 2
yaml["a"] = 0
yaml["ab"]["cd"]["ef"] + 1 # 21
yaml["ab"]["cd"]["ef"] = 3

yaml.ab.cd.ef + 1 # 4
yaml.list.add(4)
yaml.list[0] = 0

yaml.list # [0, 2, 3, 4]

yaml.n ?: "none" # none

yaml.save(path)
```
