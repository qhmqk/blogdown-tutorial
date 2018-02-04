---
title: "actionButton"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "actionbutton"
weight: 3
description: "押すことで何らかのアクションを起こすボタンです。`inputId`で指定した値は、ボタンが押される前はNULLで、押された後に0になります。押されるたびに、値が1ずつ増加します。ボタンの押下に対応するコードは、serverで`observeEvent`や`eventReactive`内に記述します。"
---

{{< highlight r >}}
actionButton(inputId, label, icon = NULL, width = NULL, ...)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|ボタンのコンテンツ。文字列を指定するとテキストラベルになり、HTMLを使って画像を指定することもできます。|
|**`icon`**|(オプションで)ボタン上に現れるアイコン|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細は`validateCssUnit`を参照|
|**`...`**|ボタンに適用する名前付きの属性|

### 説明

初期値がゼロのアクションボタンを生成し、押されるたびに値を1ずつ増やします。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

ui <- fluidPage(
  sliderInput("obs", "Number of observations", 0, 1000, 500),
  actionButton("goButton", "Go!"),
  plotOutput("distPlot")
)

server <- function(input, output) {
  output$distPlot <- renderPlot({
    # Take a dependency on input$goButton. This will run once initially,
    # because the value changes from NULL to 0.
    input$goButton

    # Use isolate() to avoid dependency on input$obs
    dist <- isolate(rnorm(input$obs))
    hist(dist)
  })
}

shinyApp(ui, server)

}
{{< /highlight >}}

* labelに画像を指定



* iconを使用





* inputIdに応じてlabelを変更






### 参照

RStudioのReference

http://shiny.rstudio.com/articles/action-buttons.html

https://shiny.rstudio.com/reference/shiny/latest/actionButton.html

