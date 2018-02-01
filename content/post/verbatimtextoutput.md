---
title: "verbatimTextOutput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Outputs"]
slug: "verbatimTextOutput"
weight: 3
description: "テキストを出力"
---


{{< highlight r >}}
verbatimTextOutput(outputId, placeholder = FALSE)
{{< /highlight >}}


### 引数

|名前|説明|
|:--|:--|
|`outputId`|値を読み込む出力変数|
|`placeholder`|出力が空または`NULL`の場合に、空の長方形が表示されるかどうかを指定します。(出力が空でないときの動作には影響しません)|

### 値

パネル内に含まれる文字通りのテキスト出力要素

### 説明

アプリケーションのページ内で文字通りのテキストとしてリアクティブな出力変数をレンダリングします。テキストには、HTMLのタグが含まれます。

### 詳細

テキストは、レンダリングよりも優先してHTMLをエスケープします。この要素は、固定幅でフォーマットされたプリントオブジェクトを保存するために`renderPrint`関数で使用されます。

{{< highlight r >}}
Examples
## Only run this example in interactive R sessions
if (interactive()) {
  shinyApp(
    ui = basicPage(
      textInput("txt", "Enter the text to display below:"),
      verbatimTextOutput("default"),
      verbatimTextOutput("placeholder", placeholder = TRUE)
    ),
    server = function(input, output) {
      output$default <- renderText({ input$txt })
      output$placeholder <- renderText({ input$txt })
    }
  )
}
{{< /highlight >}}

### 参照

https://shiny.rstudio.com/reference/shiny/1.0.5/verbatimTextOutput.html