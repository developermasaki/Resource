# About Resource
&nbsp;&nbsp;&nbsp; Resourceについての備忘録である。

## What's Resource?
&nbsp;&nbsp;&nbsp; `Resource`とは、追加ファイルや静的コンテンツのことである。

## Types of resources
&nbsp;&nbsp;&nbsp; リソースの種類ごとに、`res/`ディレクトリ内に、サブディレクトリを作り、その中にファイルを配置する。以下は、`res/`ディレクトリ内でサポートされているディレクトリの一覧である。

### `drawable/`
&nbsp;&nbsp;&nbsp; 画像ファイルを置ける。詳細は[このリンク](https://developer.android.com/guide/topics/resources/drawable-resource)を参照すること。

### `mipmap/`
&nbsp;&nbsp;&nbsp; ランチャーアイコンの密度が異なる際に使用する。詳細は[このリンク](https://developer.android.com/training/multiscreen/screendensities#mipmap)を参照すること。

### `raw/`
&nbsp;&nbsp;&nbsp; 任意のファイルをraw形式で保存できる。

### `values/`
&nbsp;&nbsp;&nbsp; 文字列、整数、色などの単純な値を含むxmlファイルを置ける。`<resources>`内の各子要素、例えば`<string>`要素はR.stringリソースを、`<color>`要素はR.colorリソースを定義できる。

### `xml/`
&nbsp;&nbsp;&nbsp; 任意のXMLファイルを置ける。

### `font/`
&nbsp;&nbsp;&nbsp; TTFなどの拡張子を持つフォントファイルを置ける。

## How to provide alternative resource?
&nbsp;&nbsp;&nbsp; 異なる画面密度に対応するdrawableリソースや、異なる言語に対応するstringリソースを提供したいときがある。その場合、以下の手順に沿って作る必要がある。
1. `res/`ディレクトリの中に、`<resources_name>-<qualifier>`という名前のディレクトリを作る。`<resources_name>`とは、先程のtypes of resourcesの中で紹介した、ディレクトリを指す。`<qualifier>`には、後で紹介する構成修飾子を指定する。
2. 各ディレクトリに、名前が全く同じファイルを保存する。

&nbsp;&nbsp;&nbsp; 注意点として、デフォルトの構成（enやjaを指定していないディレクトリ）にも、リソースを定義する必要がある。例えば、`en`や`ja`以外の言語設定がされた場合、例外が発生する可能性があるからである。


&nbsp;&nbsp;&nbsp; 構成修飾子は、以下の通りになる。

### MCC
&nbsp;&nbsp;&nbsp; SIMカードから、どの国でスマートフォンをネットと繋げているかを取得することができる。

### 言語や地域
&nbsp;&nbsp;&nbsp; 言語は`en`や`ja`といった[言語コード](https://so-zou.jp/web-app/tech/data/code/language.htm)で定義され、[ISO 3166-1 alpha2](https://ja.wikipedia.org/wiki/ISO_3166-1)の地域コードをオプションで続けて定義できる（例：`en-rUS`）。

### UIモード
&nbsp;&nbsp;&nbsp; `car`や`television`、`watch`というように、デバイスごとに設定できる。

### ナイトモード
&nbsp;&nbsp;&nbsp; `night`で夜間、`notnight`で日中用に設定できる。

### 画面の画素密度
&nbsp;&nbsp;&nbsp; `xxhdpi`というように、画面の画素密度でリソースを分けることができる。`nodpi`では、デバイスの密度に合わせて拡大縮小したくないリソースに使用できる。

## The rules of Qualifier name
&nbsp;&nbsp;&nbsp; 名前の順番は、先ほどの構成修飾子の上からの順番に従う必要がある。例えば、`drawable-night-hdpi/`はいいが、`drawable-hdpi-night/`は順番として間違っている。他のルールは、[Qualifier name rules](https://developer.android.com/guide/topics/resources/providing-resources#QualifierRules)に書いてある。

## How to create alias resources
&nbsp;&nbsp;&nbsp; 構成修飾子で、ディレクトリを分けても、必ずどちらのディレクトリにも同じリソースをコピーする必要はない。例えば、以下のように文字列リソースである`R.string.hello`を参照できる。
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="hello">Hello</string>
    <string name="hi">@string/hello</string>
</resources>
```
&nbsp;&nbsp;&nbsp;  他にも、`color`であれば`@color/`、`drawable`であれば`@drawable`というように参照できる。

## Reference
https://developer.android.com/guide/topics/resources/providing-resources

