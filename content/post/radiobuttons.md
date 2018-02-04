---
title: "radioButtons"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "radiobuttons"
weight: 3
description: "クリックして選択した項目を切り替えるラジオボタンです。"
---

{{< highlight r >}}
radioButtons(inputId, label, choices = NULL, selected = NULL, inline = FALSE, width = NULL, choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無し|
|**`choices`**|チェックボックスに表示する値のリスト。リストの要素が名前付けられている場合、値ではなく名前がユーザに表示されます。この引数を指定すると、`choiceNames`と`choiceValues`は指定できません。値は文字列で、論理値や数値などの他の型は強制的に文字列になります。|
|**`selected`**|初期状態で選択されている値。指定がない場合は、最初の値となります。|
|**`inline`**|`TRUE`なら、選択したものがインラインで(すなわち横に)表示されます。|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細はvalidateCssUnitを参照|
|**`choiceNames`**, **`choiceValues`**|名前と値のリスト。それぞれアプリケーション内で表示され、それぞれの選択したものに対応します。このため、`choiceNames`と`choiceValues`は同じ長さである必要があります。この引数を指定すると、`choices`は指定できません。単純なテキストになる`choices`ではなく、これら両引数を用いる利点は、`choiceNames`には任意の型のUIオブジェクト(タグ、アイコン、HTMLなど)を指定できる点です。例を参照|

### 値

UI定義に追加されるラジオボタンの集合

### 説明

リストから1つの項目を選択するラジオボタンの集合を生成

### 詳細

「何も選択していない」状態を表示したい場合、オプションなしを選択した`selected = character(0)`を用いたデフォルトのラジオボタンにすることが可能です。しかし、これは推奨されません。ユーザが一度選択したその状態を返す方法がユーザにないからです。代わりに、最初の選択を`c("None selected" = "")`とすることが考えられます。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {

ui <- fluidPage(
  radioButtons("dist", "Distribution type:",
               c("Normal" = "norm",
                 "Uniform" = "unif",
                 "Log-normal" = "lnorm",
                 "Exponential" = "exp")),
  plotOutput("distPlot")
)

server <- function(input, output) {
  output$distPlot <- renderPlot({
    dist <- switch(input$dist,
                   norm = rnorm,
                   unif = runif,
                   lnorm = rlnorm,
                   exp = rexp,
                   rnorm)

    hist(dist(500))
  })
}

shinyApp(ui, server)

ui <- fluidPage(
  radioButtons("rb", "Choose one:",
               choiceNames = list(
                 icon("calendar"),
                 HTML("<p style='color:red;'>Red Text</p>"),
                 "Normal text"
               ),
               choiceValues = list(
                 "icon", "html", "text"
               )),
  textOutput("txt")
)

server <- function(input, output) {
  output$txt <- renderText({
    paste("You chose", input$rb)
  })
}

shinyApp(ui, server)
}
{{< /highlight >}}

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/1.0.5/radioButtons.html