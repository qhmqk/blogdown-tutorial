---
title: "passwordInput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "passwordinput"
weight: 3
description: "入力した文字列が見えなくなるテキストボックスです。"
---

{{< highlight r >}}
passwordInput(inputId, label, value = "", width = NULL, placeholder = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無し|
|**`value`**|初期値|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細は`validateCssUnit`を参照|
|**`placeholder`**|コントロールに何を入力するのかをユーザにヒントとして表示する文字列。Internet Explorerの8と9はこのオプションをサポートしません|

### 値

UI定義に追加するテキスト入力コントロール

### 説明

パスワードを入力するためのコントロールを生成

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

ui <- fluidPage(
  passwordInput("password", "Password:"),
  actionButton("go", "Go"),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderText({
    req(input$go)
    isolate(input$password)
  })
}
shinyApp(ui, server)
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/passwordInput.html