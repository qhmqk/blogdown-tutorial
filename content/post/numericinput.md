---
title: "numericInput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "numericinput"
weight: 3
description: "数値を入力するテキストボックスで、右側に現時点の数値の大きくしたり小さくしたりするボタンがついています。"
---

{{< highlight r >}}
numericInput(inputId, label, value, min = NA, max = NA, step = NA, width = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無し|
|**`value`**|初期値|
|**`min`**|入力可能な最小値|
|**`max`**|入力可能な最大値|
|**`step`**|最小値と最大値の間のステップ幅|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細は`validateCssUnit`を参照|

### 値

UI定義に追加する数値入力コントロール

### 説明

数値を入力するためのコントロールを生成

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

ui <- fluidPage(
  numericInput("obs", "Observations:", 10, min = 1, max = 100),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderText({ input$obs })
}
shinyApp(ui, server)
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/numericInput.html