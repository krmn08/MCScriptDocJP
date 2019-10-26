# 環境設定

MCScriptの開発環境を整えるのは非常に簡単です。
Spigotで配布しているプラグインを導入し、サーバーを起動してください。
plugins/MCScriptにconfig.ymlが生成されていればOKです。

config.ymlにスクリプトの設定を記述していきます。

例
```yaml
ScriptPath: plugins/MCScript/script
Depend:
  - ProtocolLib
SoftDepend:
  - WorldEdit
Ignore:
  - ignore
  - ig/ignore.mcs
Import:
  - java.util.Arrays
  - java.util.Calender
```

#### ScriptPath
スクリプトを格納するパスを記述します。
指定されたパスのスクリプトファイルをすべて読み込みます。

#### Depend
スクリプトの依存プラグイン一覧を記述します。
スクリプトの読み込みの前に指定されたプラグインをすべて有効化します。プラグインが見つからない場合は、読み込みを中止します。

#### SoftDepend
スクリプトの依存プラグイン一覧を記述します。
Dependと違い、プラグインが見つからない場合でも読み込みを続行します。

#### Ignore
ScriptPath内の読み込まないパスを記述します。
スクリプト読み込み時、ScriptPathからの相対パスを前方一致で判定します。

#### Import
事前にインポートするクラス一覧をFQCNで記述します。
すべてのスクリプトで、指定されたクラスを利用できます。

MCScriptでは、org.bukkitパッケージ以下のすべてのクラスに加え、以下のクラスが標準でインポートされています。
- java.lang.System
- java.lang.Math
- java.lang.Object
- java.lang.StringBuilder
- java.lang.String
- java.lang.Boolean
- java.lang.Character
- java.lang.Number
- java.lang.Byte
- java.lang.Short
- java.lang.Integer
- java.lang.Float
- java.lang.Double