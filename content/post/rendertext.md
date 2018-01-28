---
title: "renderText"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["Rendering functions"]
slug: "rendertext"
weight: 3
description: "文字列をレンダリング"
---

{{< highlight r >}}
renderText(expr, env = parent.frame(), quoted = FALSE, outputArgs = list())
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|`expr`|xtableで使用可能なRのオブジェクトを返す式|
|`env`|中で`expr`を評価するための環境|
|`quoted`|`expr`に引用符が付いている(`quoted()`がある)かどうかを指定します。変数内の式を保存したいときに有用です。|
|`outputArgs`|`renderText`を、インタラクティブなR Markdownドキュメントで使用する時に、明示しない`textOutput`の呼び出しに渡される引数のリスト|

### 説明

`cat`で結果を単独要素の文字ベクトルに変える関数のリアクティブなバージョンを生成します。

### 詳細

対応するHTMLの出力タグは、何にでもなります(monospaceフォントとwhitespaceを保存するなら、`pre`が推奨されます)。そして、CSSのクラス名として`shiny-text-output`を持ちます。

関数の実行結果は、`capture.output`呼び出しの内部で`cat`に渡されます。

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

https://shiny.rstudio.com/reference/shiny/1.0.5/renderText.html

