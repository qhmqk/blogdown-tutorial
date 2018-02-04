---
title: "fileInput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "fileinput"
weight: 3
description: "a"
---

{{< highlight r >}}
fileInput(inputId, label, multiple = FALSE, accept = NULL, width = NULL, buttonLabel = "Browse...", placeholder = "No file selected")
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無し|
|**`multiple`**|ユーザが複数のファイルを同時にアップロードできるかどうかを論理値で指定します。IE9よりも古いブラウザでは動作しません。|
|**`accept`**|サーバが受け付けるファイルの種類をヒントとして与えるために、MIME型の文字ベクトル|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細はvalidateCssUnitを参照|
|**`buttonLabel`**|テキストまたはHTMLタグで指定するボタンのラベル|
|**`placeholder`**|ファイルをアップロードする前に表示するテキスト|

### 説明

1つ以上のファイルをアップロードするコントロールを生成。

### 詳細




### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

ui <- fluidPage(
  sidebarLayout(
    sidebarPanel(
      fileInput("file1", "Choose CSV File",
        accept = c(
          "text/csv",
          "text/comma-separated-values,text/plain",
          ".csv")
        ),
      tags$hr(),
      checkboxInput("header", "Header", TRUE)
    ),
    mainPanel(
      tableOutput("contents")
    )
  )
)

server <- function(input, output) {
  output$contents <- renderTable({
    # input$file1 will be NULL initially. After the user selects
    # and uploads a file, it will be a data frame with 'name',
    # 'size', 'type', and 'datapath' columns. The 'datapath'
    # column will contain the local filenames where the data can
    # be found.
    inFile <- input$file1

    if (is.null(inFile))
      return(NULL)

    read.csv(inFile$datapath, header = input$header)
  })
}

shinyApp(ui, server)
}
{{< /highlight >}}

### 参照

RStudioのリファレンス

https://shiny.rstudio.com/reference/shiny/latest/fileInput.html