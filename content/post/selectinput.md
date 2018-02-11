---
title: "selectInput"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "selectinput"
weight: 3
description: "プルダウンリストやプルダウンメニュー、ドロップダウンメニューなどの名前で呼ばれるクリックすることで、下側に選択肢が広がり、その中から1つを選択します。英語では、select list controlです。"
---

{{< highlight r >}}
selectInput(inputId, label, choices, selected = NULL, multiple = FALSE, selectize = TRUE, width = NULL, size = NULL)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無し|
|**`choices`**|チェックボックスに表示する値のリスト。リストの要素が名前付けられている場合、値ではなく名前がユーザに表示されます。この引数を指定すると、`choiceNames`と`choiceValues`は指定できません。値は文字列で、論理値や数値などの他の型は強制的に文字列になります。|
|**`selected`**|初期状態で選択されている値|
|**`multiple`**|複数の選択を許すかどうかを論理値で指定|
|**`selectize`**|selectize.jsを使うかどうかを指定|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細はvalidateCssUnitを参照|
|**`size`**|選択ボックスの中に表示する項目数を指定。大きくすると縦に長いボックスとなります。`selectize = TRUE`とは共存できません。通常、`multiple = FALSE`のときに、ドロップダウンリストとなりますが、`size`を設定すると、一つのボックスになります。|
|**`options`**|オプションのリスト。どのようなオプションを指定可能かは、selectize.jsのドキュメントを参照してください。(`I()`内の文字オプションの値はリテラルのJavaScriptコードとして扱われます。詳細は`renderDataTable()`を参照してください)|


### 値

UI定義に追加されるHTML要素のリスト。

### 説明

一つあるいは複数の項目を値のリストから選ぶための選択リストを生成。

### 詳細


Details
By default, selectInput() and selectizeInput() use the JavaScript library selectize.js (https://github.com/selectize/selectize.js) to instead of the basic select input element. To use the standard HTML select input element, use selectInput() with selectize=FALSE.

In selectize mode, if the first element in choices has a value of "", its name will be treated as a placeholder prompt. For example: selectInput("letter", "Letter", c("Choose one" = "", LETTERS))

### 注記

Note
The selectize input created from selectizeInput() allows deletion of the selected option even in a single select input, which will return an empty string as its value. This is the default behavior of selectize.js. However, the selectize input created from selectInput(..., selectize = TRUE) will ignore the empty string value when it is a single choice input and the empty string is not in the choices argument. This is to keep compatibility with selectInput(..., selectize = FALSE).

### 使用例

{{< highlight r >}}
Examples
## Only run examples in interactive R sessions
if (interactive()) {

# basic example
shinyApp(
  ui = fluidPage(
    selectInput("variable", "Variable:",
                c("Cylinders" = "cyl",
                  "Transmission" = "am",
                  "Gears" = "gear")),
    tableOutput("data")
  ),
  server = function(input, output) {
    output$data <- renderTable({
      mtcars[, c("mpg", input$variable), drop = FALSE]
    }, rownames = TRUE)
  }
)

# demoing optgroup support in the `choices` arg
shinyApp(
  ui = fluidPage(
    selectInput("state", "Choose a state:",
      list(`East Coast` = c("NY", "NJ", "CT"),
           `West Coast` = c("WA", "OR", "CA"),
           `Midwest` = c("MN", "WI", "IA"))
    ),
    textOutput("result")
  ),
  server = function(input, output) {
    output$result <- renderText({
      paste("You chose", input$state)
    })
  }
)
}
{{< /highlight >}}

### 参照

RStudioのReference

