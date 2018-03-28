---
title: "checkboxInput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "checkboxinput"
weight: 3
description: "トグルスイッチ形式のチェックボックスをUIに配置します。"
---

{{< highlight r >}}
checkboxInput(inputId, label, value = FALSE, width = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無し|
|**`value`**|初期値(論理値で`TRUE`または`FALSE`)|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細はvalidateCssUnitを参照|

### 値

UI定義に追加されるチェックボックスのコントロール。

### 説明

論理値を指定するために使用するチェックボックスを生成。

### 使用例

{{< figure src="/ui-input/checkboxinput-example.gif" alt="Simple example using checkboxInput" >}}

入力用のチェックボックスの状態を、`renderText`により文字列として出力します。

{{< highlight r >}}
ui <- fluidPage(
  checkboxInput("somevalue", "Some value", FALSE),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderText({ input$somevalue })
}
shinyApp(ui, server)
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/latest/checkboxInput.html