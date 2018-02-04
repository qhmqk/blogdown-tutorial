---
title: "renderUI"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["Rendering functions"]
slug: "renderui"
weight: 3
description: "HTMLで書かれたオブジェクトなどをレンダリング"
---

{{< highlight r >}}
renderUI(expr, env = parent.frame(), quoted = FALSE, outputArgs = list())
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`expr`**|Shinyのタグオブジェクト、HTML、またはそれらのリストを返す式|
|**`env`**|中で`expr`を評価するための環境|
|**`quoted`**|`expr`に引用符が付いている(`quoted()`がある)かどうかを指定します。変数内の式を保存したいときに有用です。|
|**`outputArgs`**|`renderUI`を、インタラクティブなR Markdownドキュメントで使用する時に、明示しない`uiOutput`の呼び出しに渡される引数のリスト|

### 説明

実験的な機能です。ShinyのUIライブラリを用いてHTMLを生成する関数のリアクティブなバージョンを生成します。

### 詳細

出力するHTMLの出力タグは`div`で、CSSのクラス名に`shiny-html-output`を持ちます(または`uiOutput`を使用します)。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

ui <- fluidPage(
  uiOutput("moreControls")
)

server <- function(input, output) {
  output$moreControls <- renderUI({
    tagList(
      sliderInput("n", "N", 1, 1000, 500),
      textInput("label", "Label")
    )
  })
}
shinyApp(ui, server)
}
{{< /highlight >}}

### 参照

https://shiny.rstudio.com/reference/shiny/1.0.5/renderUI.html