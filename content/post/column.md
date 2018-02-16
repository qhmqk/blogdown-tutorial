---
title: "column"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "cokumn"
weight: 3
description: "UI定義内に列を生成"
---

{{< highlight r >}}
column(width, ..., offset = 0)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`width`**|列のグリッド幅を1～12の値で指定|
|**`...`**|列内の要素|
|**`offset`**|前の列の終わりからその列までのオフセットとなる列の数|

### 値

`fluidRow`または`fixedRow`内に含まれる列

### 詳細

`fluidRow`または`fixedRow`内で用いられる列を生成

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

ui <- fluidPage(
  fluidRow(
    column(4,
      sliderInput("obs", "Number of observations:",
                  min = 1, max = 1000, value = 500)
    ),
    column(8,
      plotOutput("distPlot")
    )
  )
)

server <- function(input, output) {
  output$distPlot <- renderPlot({
    hist(rnorm(input$obs))
  })
}

shinyApp(ui, server)



ui <- fluidPage(
  fluidRow(
    column(width = 4,
      "4"
    ),
    column(width = 3, offset = 2,
      "3 offset 2"
    )
  )
)
shinyApp(ui, server = function(input, output) { })
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/column.html
