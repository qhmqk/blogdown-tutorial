---
title: "sidebarLayout"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "sidebarlayout"
weight: 3
description: "サイドバーとメインの領域を持つレイアウトを生成。サイドバーは、メインとは違う背景色で表示され、入力コントロールが配置されます。メインは、水平方向で2/3の幅を持ち、出力コントロールが配置されます。"
---

{{< highlight r >}}
sidebarLayout(sidebarPanel, mainPanel, position = c("left", "right"), fluid = TRUE)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`sidebarPanel`**|入力コントロールを要素として持つサイドバーのパネル|
|**`mainPanel`**|出力を要素として持つメインパネル|
|**`position`**|サイドバーとメインの位置を"left"または"right"で指定|
|**`fluid`**|`TRUE`なら可変レイアウト、`FALSE`なら固定レイアウト|

### 説明

サイドバーとメインの領域を持つレイアウトを生成。サイドバーは、メインとは違う背景色で表示され、入力コントロールが配置されます。メインは、水平方向で2/3の幅を持ち、出力コントロールが配置されます。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {
options(device.ask.default = FALSE)

# Define UI
ui <- fluidPage(

  # Application title
  titlePanel("Hello Shiny!"),

  sidebarLayout(

    # Sidebar with a slider input
    sidebarPanel(
      sliderInput("obs",
                  "Number of observations:",
                  min = 0,
                  max = 1000,
                  value = 500)
    ),

    # Show a plot of the generated distribution
    mainPanel(
      plotOutput("distPlot")
    )
  )
)

# Server logic
server <- function(input, output) {
  output$distPlot <- renderPlot({
    hist(rnorm(input$obs))
  })
}

# Complete app with UI and server components
shinyApp(ui, server)
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/sidebarLayout.html