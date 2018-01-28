---
title: "renderTable"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["Rendering functions"]
slug: "rendertable"
weight: 3
description: "DT::renderDataTableを使った方がいいでしょう。"
---

{{< highlight r >}}
renderTable(expr, striped = FALSE, hover = FALSE, bordered = FALSE, spacing = c("s", "xs", "m", "l"), width = "auto", align = NULL,
  rownames = FALSE, colnames = TRUE, digits = NULL, na = "NA", ..., env = parent.frame(), quoted = FALSE, outputArgs = list())
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|`expr`|xtableで使用可能なRのオブジェクトを返す式|
|`striped`, `hover`, `bordered`|論理値で、`TRUE`なら出力する表に対応するBootstrapの表フォーマットを適用します。|
|`spacing`|表の行間のスペースを指定します。`xs`は「extra small」の略で、`s`は「small」、`m`は「medum」で、`l`は「large」です。|
|`width`|表の幅。CSSの単位(100やauto)、またはpxを単位にした長さを指定する文字列|
|`align`|列のアラインメントを文字列で指定します。`l`, `c`, `r`でそれぞれ列の左、中央右にアラインメントされます。文字列の長さは、表と同じになります(`rawnames = TRUE`なら、`ncol()+1`)。i番目の文字が、i番目の列に対応します。`?`を指定することも可能で、デフォルトのアラインメントを指定することになります。`NULL`なら、数値の列はすべて右に、その他はすべて左になります(`?`を指定した場合も同様です)。|
|`rownames`, `colnames`|論理値で行名や列名を含めるかどうかを指定します。|
|`digits`|数値の列の桁数を整数で指定します(整数クラスの列には適用されません)。負の数を指定すると、数値の列が絶対値で`digits`で指定した少数の精度で表示されます。|
|`na`|欠損値となっている表のセルに用いる文字列を指定します。NAまたは、NaNとして評価されます。|
|`...`|`xtable`と`print.xtable`に渡される引数|
|`env`|中で`expr`を評価するための環境|
|`quoted`|`expr`に引用符が付いている(`quoted()`がある)かどうかを指定します。変数内の式を保存したいときに有用です。|
|`width`|`options('width')`の値|
|`outputArgs`|`renderTable`を、インタラクティブなR Markdownドキュメントで使用する時に、明示しない`tableOutput`の呼び出しに渡される引数のリスト|

### 説明

出力スロットに割り当てるのに適したリアクティブな表を生成

### 詳細

`div`に対応するHTMLの出力タグで、CSSのクラス名は`shiny-html-output`です。

### 参照

https://shiny.rstudio.com/reference/shiny/1.0.5/renderTable.html
