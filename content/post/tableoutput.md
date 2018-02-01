---
title: "tableOutput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Outputs"]
slug: "tableoutput"
weight: 3
description: "表を出力"
---

{{< highlight r >}}
tableOutput(outputId)
{{< /highlight >}}


### 引数

|名前|説明|
|:--|:--|
|**`outputId`**|表を読み込む出力変数|

### 値

パネル内に含まれる表出力要素

### 説明

アプリケーションページ内で、`renderTable`または`renderDataTable`をレンダリングします。`renderTable`は標準的なHTMLの表を使用します。`renderDataTable`は、JavascriptライブラリのDataTablesをインタラクティブでさらに機能を持つ表を生成するために使用します。

### 使用例

{{< highlight r >}}
## Only run this example in interactive R sessions
if (interactive()) {
  # table example
  shinyApp(
    ui = fluidPage(
      fluidRow(
        column(12,
          tableOutput('table')
        )
      )
    ),
    server = function(input, output) {
      output$table <- renderTable(iris)
    }
  )


  # DataTables example
  shinyApp(
    ui = fluidPage(
      fluidRow(
        column(12,
          dataTableOutput('table')
        )
      )
    ),
    server = function(input, output) {
      output$table <- renderDataTable(iris)
    }
  )
}
{{< /highlight >}}

### 参照

https://shiny.rstudio.com/reference/shiny/1.0.5/tableOutput.html