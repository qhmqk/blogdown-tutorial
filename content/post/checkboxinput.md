---
title: "checkboxInput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["control widgets"]
slug: "checkboxinput"
weight: 3
description: "論理値を指定するために使用するチェックボックスを生成"
---

```r
checkboxInput(inputId, label, value = FALSE, width = NULL)
```

### 引数

|名前|説明|
|:--|:--|
|inputId|値にアクセスするために使用する`input`のスロット|
|label|コントロールに表示するラベル。`NULL`ならラベル無し|
|value|初期値(論理値で`TRUE`または`FALSE`)|
|width|'400px'や'100%'などの形式で幅を指定。詳細はvalidateCssUnitを参照|

### 値

UI定義に追加されるチェックボックスのコントロール。

### 説明

論理値を指定するために使用するチェックボックスを生成。

### 使用例

```{r eval = FALSE}
## Only run examples in interactive R sessions
if (interactive()) {
ui <- fluidPage(
  checkboxInput("somevalue", "Some value", FALSE),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderText({ input$somevalue })
}
shinyApp(ui, server)
}
```

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/latest/checkboxInput.html