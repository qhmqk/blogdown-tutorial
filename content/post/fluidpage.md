---
title: "fluidPage"
author: "qhmqk"
date: 2018-02-12
categories: ["Shiny"]
tags: ["UI Layout"]
slug: "fluidpage"
weight: 3
description: "可変レイアウトのページを生成"
---

{{< highlight r >}}
fluidPage(..., title = NULL, responsive = NULL, theme = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`...`**|ページ内の要素|
|**`title`**|ブラウザウィンドウに表示されるタイトル(デフォルトではページがホストされたURL)。`titlePanel`関数でも設定可能です。|
|**`responsive`**|このオプションは推奨されません。Bootstrap 3のオプションにもう無いからです。|
|**`theme`**|Bootstrapのスタイルシート。通常は、wwwディレクトリ内にCSSファイルで定義したものを指定します。例えば、www/bootstrap.cssで置いたテーマを用いる場合、`theme = "bootstrap.css"`を指定します。|

### 値

`shinyUI`関数に渡されるUI定義

### 説明

可変ページレイアウトを生成する関数です。可変ページレイアウトは、行と行に順番に含まれる列から構成されます。行は要素が(ブラウザに十分な幅があるなら)同じ行に現れるようにする目的で存在します。列は水平に12分割したグリッドで要素がどれだけを占めるのかを定義する目的で存在します。可変ページは利用可能なブラウザの幅すべてを埋めるためにリアルタイムで拡大縮小します。

### 詳細

可変ページの生成には、`fluidPage`関数を用いて、`fluidRow`とその中の`column`のインスタンスを同梱します。低級な行と列関数の代わりとして、`sidebarLayout`のような高級レイアウト関数を使用可能です。

### 注記

可変ページにレイアウトするときのさらなる詳細は、Shiny-Applicatin-Layout-Guideを参照してください。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

# Example of UI with fluidPage
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
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/fluidPage.html
