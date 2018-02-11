---
title: "numericInput"
author: "qhmqk"
date: 2018-02-09
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

#### もっとも基本的な使い方

1から100までの数値を入力し、その数値を[`verbatimTextOutput`]({{< ref "verbatimtextoutput.md" >}})で表示します。

{{< highlight r >}}
library(shiny)

ui <- fluidPage(
  numericInput("obs", "Observations:", 10, min = 1, max = 100),
  verbatimTextOutput("value")
)

server <- function(input, output) {
  output$value <- renderText({ input$obs })
}

shinyApp(ui, server)
{{< /highlight >}}

#### 埋め込みCSSを使ったサイズ変更

UIの`fluidPage`に、`tags`でCSSを埋め込んでサイズを変更します。

{{< highlight r >}}
tags$head(
  tags$style(HTML("#obs{width: 100px;}"))
),
{{< /highlight >}}

#### 埋め込みCSSによる複数の`numericInput`の一括サイズ変更

`#obs`ではなく、`input[type=\"number\"]`とすることで、すべての`numericInput`をまとめてCSSでサイズ変更する対象とします。

{{< highlight r >}}
library(shiny)

ui <- fluidPage(
  tags$head(
    tags$style(HTML("input[type=\"number\"] {width: 100px;}"))
  ),
  numericInput("obs1", "Observations1:", 10, min = 1, max = 100),
  numericInput("obs2", "Observations2:", 10, min = 1, max = 100),
  h4("Obs1 + Obs2"),
  verbatimTextOutput("value")
)

server <- function(input, output) {
  output$value <- renderText({ input$obs1 + input$obs2 })
}

shinyApp(ui, server)
{{< /highlight >}}

#### スピンボタン(セレクタ)なしの数値入力

スピンボタン(セレクタ)により、キーボードからの直接入力に加えて右側のボタンでも数値を変更できます。このボタンを取り除くオプションは`numericInput`にはありません。身も蓋もありませんが、[`textInput`]({{< ref "textinput.md" >}})を代用することにより、スピンボタン(セレクタ)なしの数値入力を実現できます。

{{< highlight r >}}
library(shiny)

ui <- fluidPage(
  textInput("obs", "Observations:", "10"),
  verbatimTextOutput("value")
)

server <- function(input, output) {
  num <- reactive({as.numeric(input$obs)})
  output$value <- renderText({ num() })
}

shinyApp(ui, server)
{{< /highlight >}}

`as.numeric`は、数値以外の文字列が入力されると`NA`を返します。最小や最大を指定する場合は、`num <- reactive({as.numeric(input$obs)})`にif文の判定を追加します。

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/numericInput.html

Stackoverflow

https://stackoverflow.com/questions/29811301/r-shiny-resize-numericinput-box