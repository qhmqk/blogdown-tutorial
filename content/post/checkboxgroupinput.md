---
title: "checkboxGroupInput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
weight: 3
slug: "checkboxgroupinput"
description: "トグルスイッチ形式の複数のチェックボックスをUIに配置します。"
---

{{< highlight r >}}
checkboxGroupInput(inputId, label, choices = NULL, selected = NULL, inline = FALSE, width = NULL, choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無し|
|**`choices`**|チェックボックスに表示する値のリスト。リストの要素が名前付けられている場合、値ではなく名前がユーザに表示されます。この引数を指定すると、`choiceNames`と`choiceValues`は指定できません。値は文字列で、論理値や数値などの他の型は強制的に文字列になります。|
|**`selected`**|初期状態で選択されている値|
|**`inline`**|`TRUE`なら、選択したものがインラインで表示されます。|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細はvalidateCssUnitを参照|
|**`choiceNames`**, **`choiceValues`**|名前と値のリスト。それぞれアプリケーション内で表示され、それぞれの選択したものに対応します。このため、`choiceNames`と`choiceValues`は同じ長さである必要があります。この引数を指定すると、`choices`は指定できません。単純なテキストになる`choices`ではなく、これら両引数を用いる利点は、`choiceNames`には任意の型のUIオブジェクト(タグ、アイコン、HTMLなど)を指定できる点です。例を参照|

### 値

UI定義に追加されるHTML要素のリスト

### 説明

それぞれ独立で選択できるトグルスイッチ形式のチェックボックスの組を生成します。選択された値の文字列ベクトルが、入力としてサーバに渡されます。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {
ui <- fluidPage(
  checkboxGroupInput("variable", "Variables to show:",
                     c("Cylinders" = "cyl",
                       "Transmission" = "am",
                       "Gears" = "gear")),
  tableOutput("data")
)
server <- function(input, output, session) {
  output$data <- renderTable({
    mtcars[, c("mpg", input$variable), drop = FALSE]
  }, rownames = TRUE)
}
shinyApp(ui, server)
ui <- fluidPage(
  checkboxGroupInput("icons", "Choose icons:",
    choiceNames =
      list(icon("calendar"), icon("bed"),
           icon("cog"), icon("bug")),
    choiceValues =
      list("calendar", "bed", "cog", "bug")
  ),
  textOutput("txt")
)
server <- function(input, output, session) {
  output$txt <- renderText({
    icons <- paste(input$icons, collapse = ", ")
    paste("You chose", icons)
  })
}
shinyApp(ui, server)
}
{{< /highlight >}}


* `choices`

* `inline`を`TRUE`

### 参照

RStudioのReference

https://shiny.rstudio.com/reference/shiny/latest/checkboxGroupInput.html