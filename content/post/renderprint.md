---
title: "renderPrint"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["Rendering functions"]
slug: "renderprint"
weight: 3
description: "文字列をレンダリング"
---

作成中
{{< highlight r >}}
renderPrint(expr, env = parent.frame(), quoted = FALSE, width = getOption("width"), outputArgs = list())
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|`expr`|出力を印字、または印字可能なRオブジェクトを返す式|
|`env`|中で`expr`を評価するための環境|
|`quoted`|`expr`に引用符が付いている(`quoted()`がある)かどうかを指定します。変数内の式を保存したいときに有用です。|
|`width`|`options('width')`の値|
|`outputArgs`|`renderPrint`を、インタラクティブなR Markdownドキュメントで使用する時に、明示しない`verbatimTextOutput`の呼び出しに渡される引数のリスト|

#### 説明

印字する出力をキャプチャする関数のリアクティブなバージョンを生成します。また、印字可能な出力を(見えなかったとしても)キャプチャし、文字列にします。結果の関数は、出力スロットへの割当に適しています。

### 詳細

対応するHTML出力タグは、任意で何にでも成り(monospaceフォントとwhitespaceをpreserveしたいなら、preが推奨されます)、CSSのクラス名は`shiny-text-output`を持ちます。

関数の実行結果は、`capture.output`呼び出しの内部で印字されます。

大半のShinyの出力関数と違い、`NULL`も`NULL`であることが見えるように出力されます。`NULL`で何も表示しないためには、関数が`invisible()`を返すようにしなければならないことにちゅうしてください。

### 使用例

{{< highlight r >}}
isolate({

# renderPrint captures any print output, converts it to a string, and
# returns it
visFun <- renderPrint({ "foo" })
visFun()
# '[1] "foo"'

invisFun <- renderPrint({ invisible("foo") })
invisFun()
# ''

multiprintFun <- renderPrint({
  print("foo");
  "bar"
})
multiprintFun()
# '[1] "foo"\n[1] "bar"'

nullFun <- renderPrint({ NULL })
nullFun()
# 'NULL'

invisNullFun <- renderPrint({ invisible(NULL) })
invisNullFun()
# ''

vecFun <- renderPrint({ 1:5 })
vecFun()
# '[1] 1 2 3 4 5'


# Contrast with renderText, which takes the value returned from the function
# and uses cat() to convert it to a string
visFun <- renderText({ "foo" })
visFun()
# 'foo'

invisFun <- renderText({ invisible("foo") })
invisFun()
# 'foo'

multiprintFun <- renderText({
  print("foo");
  "bar"
})
multiprintFun()
# 'bar'

nullFun <- renderText({ NULL })
nullFun()
# ''

invisNullFun <- renderText({ invisible(NULL) })
invisNullFun()
# ''

vecFun <- renderText({ 1:5 })
vecFun()
# '1 2 3 4 5'

})

[1] "foo"

[1] "1 2 3 4 5"
{{< /highlight >}}

### 参照

https://shiny.rstudio.com/reference/shiny/1.0.5/renderPrint.html

