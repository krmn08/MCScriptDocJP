# ビルトイン関数

|関数名|引数|説明|
|---|---|---|
|Print|Object|オブジェクトをコンソールに出力する|
|Println|Object|オブジェクトをコンソールに出力して改行する|
|ToString|Object|多次元配列に対応したToString|
|Cast|ClassObject, Number|数値を指定した型にキャストする|
|Int|Character|CharacterをIntegerにキャストする|
|Char|Integer|IntegerをCharacterにキャストする|
|Array|ClassObject, Integer...|指定された型と各次元のサイズで配列を生成する|
|Array|ClassObject, List|リストを指定された型の配列に変換する|
|Array|ClassObject, List, Function|リストを指定された型の配列に関数を使って変換する|
|Add|Collection, Object|コレクションにオブジェクトを追加する|
|Remove|List, Integer|指定されたインデックスの要素をリストから削除する|
|Remove|Collection, Object|指定された要素をコレクションから削除する|
|Length|Object|配列、または文字列の長さを取得する|
|Field|Object|プロパティ名と値のマップを返す。ClassObjectが渡された場合、プロパティ名と値の型のマップを返す|
|Iota|Integer|Iota内部の値を指定された値で初期化し、値を返す|
|Iota|-|Iota内部の値をインクリメントして返す|
|Load|String|指定されたファイルのYamlConfigurationを返す|
|ExecTime|Function|指定された関数の実行時間を返す(ms)|