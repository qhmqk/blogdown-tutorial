---
title: "shinywidgets"
author: "qhmqk"
date: 2018-03-27
categories: ["Shiny"]
tags: ["Packages"]
slug: "shinywidgets"
weight: 3
description: "入出力ウィジェットを作成"
toc: true
---

### actionBttn

{{< highlight r >}}
actionBttn(inputId, label = NULL, icon = NULL, style = "unite", color = "default", size = "md", block = FALSE, no_outline = TRUE)
{{< /highlight >}}

#### actionBttnの説明

Awesomeのアクションボタンです。`actionButton`に似ていますが、https://bttn.surge.sh/ で提供されるリッチな表現のボタンが使用可能です。

#### actionBttnの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするときに用いる入力のスロット。|
|**`label`**|ボタンのコンテンツで、通常はテキストのラベルです。|
|**`icon`**|ボタンの上に現れるオプションのアイコン。|
|**`style`**|ボタンのスタイルを指定。`simple`, `bordered`, `minimal`, `stretch`, `jelly`, `gradient`, `fill`, `material-circle`, の中から選択します。|
|**`color`**|ボタンの色。`default`, `primary`, `warning`, `danger`, `success`, `royal`の中から選択します。|
|**`size`**|ボタンのサイズ。単位には`xs`, `sm`, `md`, `lg`のいずれかを使用します。|
|**`block`**|ボタンの幅をいっぱいにするかどうかを論理値で指定。|
|**`no_outline`**|キーボード、またはマウスやタッチを用いてナビゲートするときに枠を表示するかどうかを論理値で指定。|

#### actionBttnの使用例

{{< figure src="/ui-input/shinywidgets-actionbttn.gif" alt="actionBttn" >}}

{{< highlight r >}}
ui <- fluidPage(
  actionBttn(inputId = "id1", label = "Go!", style = "unite")
)
server <- function(input, output, session) {
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}

### actionGroupButtons

{{< highlight r >}}
actionGroupButtons(inputIds, labels, status = "default", size = "normal", direction = "horizontal", fullwidth = FALSE)
{{< /highlight >}}

#### actionGroupButtonsの説明

アクションボタンをグループ化した入力を生成します。

#### actionGroupButtonsの引数

|名前|説明|
|:--|:--|
|**`inputIds`**|値にアクセスするときに用いる入力のスロット。一つ一つの値がそれぞれのボタンに対応します。|
|**`labels`**|各ボタンのラベル。大きさは`inputIds`と同じである必要があります。|
|**`status`**|ボタンにクラスを追加します。`info`, `primary`, `danger`, `warning`, `success`などのBootstrapのステータスを使用可能です。または、`status = 'myClass'`のように任意の文字列を指定することで、ボタンにクラス`btn-myClass`を持たせます。|
|**`size`**|ボタンのサイズ(’xs’, ’sm’, ’normal’, ’lg’)|
|**`direction`**|`horizontal`(水平)または`vertical`(垂直)を指定します。|
|**`fullwidth`**|`TRUE`の場合、親の`<div>`の幅を埋めます。|

#### actionGroupButtonsの値

UI定義に追加するアクションボタンのグループコントロール。

#### actionGroupButtonsの使用例

{{< figure src="/ui-input/shinywidgets-actiongroupbuttons.png" alt="actionGroupButtons" >}}

{{< highlight r >}}
ui <- fluidPage(
  br(),
  actionGroupButtons(
    inputIds = c("btn1", "btn2", "btn3"),
    labels = list("Action 1", "Action 2", tags$span(icon("gear"), "Action 3")),
    status = "primary"
  ),
  verbatimTextOutput(outputId = "res1"),
  verbatimTextOutput(outputId = "res2"),
  verbatimTextOutput(outputId = "res3")
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$btn1)
  output$res2 <- renderPrint(input$btn2)
  output$res3 <- renderPrint(input$btn3)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}

### animateOptions

{{< highlight r >}}
animateOptions(enter = "fadeInDown", exit = "fadeOutUp", duration = 1)
{{< /highlight >}}

#### animateOptionsの説明

アニメーションのオプション。

#### animateOptionsの引数

|名前|説明|
|:--|:--|
|**`enter`**|表示するアニメーションの名前|
|**`exit`**|表示が消えるアニメーションの名前|
|**`duration`**|アニメーションの間隔|

#### animateOptionsの値

リスト

#### animateOptionsの使用例

{{< highlight r >}}
dropdown(
  "Your contents goes here ! You can pass several elements",
  circle = TRUE, status = "danger", icon = icon("gear"), width = "300px",
  animate = animateOptions(enter = "fadeInDown", exit = "fadeOutUp", duration = 3)
)
{{< /highlight >}}


