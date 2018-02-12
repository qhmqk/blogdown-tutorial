---
title: "splitLayout"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "splitlayout"
weight: 3
description: "`要素を水平に等しく２分割に配置します。"
---

{{< highlight r >}}
splitLayout(..., cellWidths = NULL, cellArgs = list())
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|名前の指定されていない引数は、レイアウトの子要素になります。名前の付いた引数は最も外側のタグのHTML属性になります。|
|**`callWidths`**|それぞれのセルの幅を指定する文字または数値のベクトル。必要に応じて、再利用がなされます。文字の値はCSSの長さとして解釈されます(`validateCssUnit`を参照してください)。数値の値は、ピクセルとして解釈されます。|
|**`callArgs`**|レイアウトの隠せるで用いられる任意の追加属性|

### 説明

要素を水平に等しく２分割に配置します。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {
options(device.ask.default = FALSE)

# Server code used for all examples
server <- function(input, output) {
  output$plot1 <- renderPlot(plot(cars))
  output$plot2 <- renderPlot(plot(pressure))
  output$plot3 <- renderPlot(plot(AirPassengers))
}

# Equal sizing
ui <- splitLayout(
  plotOutput("plot1"),
  plotOutput("plot2")
)
shinyApp(ui, server)

# Custom widths
ui <- splitLayout(cellWidths = c("25%", "75%"),
  plotOutput("plot1"),
  plotOutput("plot2")
)
shinyApp(ui, server)

# All cells at 300 pixels wide, with cell padding
# and a border around everything
ui <- splitLayout(
  style = "border: 1px solid silver;",
  cellWidths = 300,
  cellArgs = list(style = "padding: 6px"),
  plotOutput("plot1"),
  plotOutput("plot2"),
  plotOutput("plot3")
)
shinyApp(ui, server)
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/splitLayout.html
