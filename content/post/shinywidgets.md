---
title: "shinyWidgets"
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


### animations

アニメーションの名前

#### animationsの説明

カテゴリごとの全てのアニメーションのリスト

#### animationsのフォーマット

リストのリスト

#### animationsのソース

https://github.com/daneden/animate.css/blob/master/animate-config.json



### awesomeCheckbox

{{< highlight r >}}
awesomeCheckbox(inputId, label, value = FALSE, status = "primary", width = NULL)
{{< /highlight >}}

#### awesomeCheckboxの説明

Awesomeのチェックボックス入力のコントロールで、論理値を指定するためのAwesome Bootstrapのチェックボックスを生成します。

#### awesomeCheckboxの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|入力のラベル|
|**`value`**|初期値を論理値(`TRUE`または`FALSE`)で指定|
|**`status`**|ボタンの色をBootstrapのステータス(`default`, `primary`, `info`, `success`, `warning`, `danger`)で指定|
|**`width`**|入力の幅|

#### awesomeCheckboxの値

UI定義に追加するチェックボックスのコントロール

#### awesomeCheckboxの使用例

{{< figure src="/ui-input/shinywidgets-awesomecheckbox.png" alt="awesomeCheckbox" >}}

{{< highlight r >}}
ui <- fluidPage(
  awesomeCheckbox(inputId = "somevalue",
                  label = "A single checkbox",
                  value = TRUE,
                  status = "danger"),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderText({ input$somevalue })
}
shinyApp(ui, server)
{{< /highlight >}}


### awesomeCheckboxGroup

awesomecheckboxのグループの入力コントロール

{{< highlight r >}}
awesomeCheckboxGroup(inputId, label, choices, selected = NULL, inline = FALSE, status = "primary", width = NULL)
{{< /highlight >}}

#### awesomeCheckboxGroupの説明

論理値を指定するために用いられるFont AwesomeのBootstrapチェックボックスを生成

#### awesomeCheckboxGroupの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|入力のラベル|
|**`choices`**|チェックボックスに表示する値のリスト|
|**`selected`**|初期値として選択されている値|
|**`inline`**|`TRUE`の場合、選択肢をインライン(すなわち水平)にレンダリングします。|
|**`status`**|ボタンの色|
|**`width`**|入力の幅|

#### awesomeCheckboxGroupの値

UI定義に追加するチェックボックスのコントロール

#### awesomeCheckboxGroupの使用例

{{< figure src="/ui-input/shinywidgets-awesomecheckboxgroup.png" alt="awesomeCheckboxGroup" >}}

{{< highlight r >}}
ui <- fluidPage(
  br(),
  awesomeCheckboxGroup(
    inputId = "id1", label = "Make a choice:",
    choices = c("graphics", "ggplot2")
  ),
  verbatimTextOutput(outputId = "res1"),
  br(),
  awesomeCheckboxGroup(
    inputId = "id2", label = "Make a choice:",
    choices = c("base", "dplyr", "data.table"),
    inline = TRUE, status = "danger"
  ),
  verbatimTextOutput(outputId = "res2")
)
server <- function(input, output, session) {
  output$res1 <- renderPrint({
    input$id1
  })
  output$res2 <- renderPrint({
    input$id2
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### awesomeRadio

{{< highlight r >}}
awesomeRadio(inputId, label, choices, selected = NULL, inline = FALSE, status = "primary", checkbox = FALSE, width = NULL)
{{< /highlight >}}

#### awesomeRadioの説明

Awesomeのラジオボタン入力のコントロールで、リストから項目を選択するために用いられるラジオボタンの集合を生成します。

#### awesomeRadioの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`choices`**|選択する値のリスト。リストの要素に名前がある場合、値ではなく名前がユーザに表示されます。|
|**`selected`**|初期値で選択されている値(指定がない場合は最初の値)。|
|**`inline`**|`TRUE`の場合、選択肢をインライン(すなわち水平)にレンダリングします。|
|**`status`**|ボタンの色をBootstrapのステータス(`default`, `primary`, `info`, `success`, `warning`, `danger`)で指定|
|**`checkbox`**|論理値でチェックボックスのような四角い形のラジオボタンを描画するかどうかを指定|
|**`width`**|入力の幅。例えば`400px`や`100%`のように指定します。|

#### awesomeRadioの値

UI定義に追加するラジオボタンの集合

#### awesomeRadioの使用例

{{< figure src="/ui-input/shinywidgets-awesomeradio.png" alt="awesomeRadio" >}}

{{< highlight r >}}
ui <- fluidPage(
  br(),
  awesomeRadio(
    inputId = "id1", label = "Make a choice:",
    choices = c("graphics", "ggplot2")
  ),
  verbatimTextOutput(outputId = "res1"),
  br(),
  awesomeRadio(
    inputId = "id2", label = "Make a choice:",
    choices = c("base", "dplyr", "data.table"),
    inline = TRUE, status = "danger"
  ),
  verbatimTextOutput(outputId = "res2")
)
server <- function(input, output, session) {
  output$res1 <- renderPrint({
    input$id1
  })
  output$res2 <- renderPrint({
    input$id2
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}


### checkboxGroupButtons

{{< highlight r >}}
checkboxGroupButtons(inputId, label = NULL, choices = NULL, selected = NULL, status = "default", size = "normal", direction = "horizontal", justified = FALSE, individual = FALSE, checkIcon = list(), width = NULL, choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

#### checkboxGroupButtonsの説明

チェックボックスのように動作するグループ化されたボタンを生成します。

#### checkboxGroupButtonsの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|入力のラベル|
|**`choices`**|選択する値のリスト。リストの要素に名前がある場合、値ではなく名前がユーザに表示されます。|
|**`selected`**|初期値で選択されている値|
|**`status`**|ボタンにクラスを追加します。`info`, `primary`, `danger`, `warning`, `success`などのBootstrapのステータスを使用可能です。または、`status = 'myClass'`のように任意の文字列を指定することで、ボタンにクラス`btn-myClass`を持たせます。|
|**`size`**|ボタンのサイズ(’xs’, ’sm’, ’normal’, ’lg’)|
|**`direction`**|`horizontal`(水平)または`vertical`(垂直)を指定します。|
|**`justified`**|`TRUE`の場合、親の`<div>`の幅を埋めます。|
|**`individual`**|`TRUE`の場合、ボタンが分かれます。|
|**`checkIcon`**|少なくとも１つは空でない要素が含まれるリスト。ボタンがチェックされた場合に表示するアイコンを指定します。|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|
|**`choiceNames`, `choiceValues`**|名前と値のリスト。それぞれアプリケーション内でユーザに各選択肢に対応するものが表示されます。このため、`choiceNames`と`choiceValues`は長さが同じである必要があります。|

#### checkboxGroupButtonsの値

UI定義に追加するボタンのグループコントロール

#### checkboxGroupButtonsの使用例

{{< figure src="/ui-input/shinywidgets-checkboxgroupbuttons.gif" alt="checkboxGroupButtons" >}}

{{< highlight r >}}
ui <- fluidPage(
  checkboxGroupButtons(inputId = "somevalue",
                       label = "Make a choice: ",
                       choices = c("A", "B", "C")),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderText({ input$somevalue })
}
shinyApp(ui, server)
{{< /highlight >}}


### circleButton

{{< highlight r >}}
circleButton(inputId, icon = NULL, status = "default", size = "default", ...)
{{< /highlight >}}

#### circleButtonの説明

丸いアクションボタンを生成します。

#### circleButtonの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`icon`**|ボタン上に現れるアイコン|
|**`status`**|ボタンの色|
|**`size`**|ボタンのサイズ(’default’, ’xs’, ’sm’, ’lg’)|
|**`...`**|ボタンに適用される名前付きの属性|


### closeSweetAlert

closeSweetAlert(session)

#### closeSweetAlertの説明

Close Sweet Alertを生成します。

#### closeSweetAlertの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|


### colorSelectorInput

{{< highlight r >}}
colorSelectorInput(inputId, label, choices, selected = NULL, mode = c("radio", "checkbox"), display_label = FALSE, ncol = 10)
{{< /highlight >}}

{{< highlight r >}}
colorSelectorExample()
{{< /highlight >}}

{{< highlight r >}}
colorSelectorDrop(inputId, label, choices, selected = NULL, display_label = FALSE, ncol = 10, circle = TRUE, size = "sm", up = FALSE, width = NULL)
{{< /highlight >}}

#### colorSelectorInputの説明

限定色の集合から色を選択します。

#### colorSelectorInputの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`choices`**|色のリスト。名前付きのリストも可能です、例を参照してください。|
|**`selected`**|デフォルトで選択されている色。`NULL`の場合、`mode = 'radio`では最初の色となり、`mode = 'checkbox'`では無しとなります。|
|**`mode`**|`radio`だとラジオボタンのように一つの値を選択し、`checkbox`だと複数の値を選択します。|
|**`display_label`**|色のパレットの後にリストの名前を表示します。|
|**`ncol`**|選択肢がリストでなくベクトルの場合に、n個の要素の後でラインに移動します。|
|**`circle`**|論理値で丸または四角のボタンの使用を指定します。|
|**`size`**|ボタンのサイズ(’default’, ’xs’, ’sm’, ’lg’)|
|**`up`**|論理値で上部にドロップダウンメニューを表示するかどうかを指定します。|
|**`width`**|ドロップダウンメニューコンテンツの幅|

#### colorSelectorInputの値

色を選択する入力コントロール

#### colorSelectorInputの関数

* colorSelectorExample: `colorSelectorInput`の使用例

* colorSelectorDrop: ドロップダウンボタンで色の選択を表示

#### colorSelectorInputの使用例

{{< figure src="/ui-input/shinywidgets-colorselectorinput.gif" alt="colorSelectorInput" >}}

{{< highlight r >}}
colorSelectorExample()
# Simple example
ui <- fluidPage(
  colorSelectorInput(
    inputId = "mycolor1", label = "Pick a color :",
    choices = c("steelblue", "cornflowerblue",
                "firebrick", "palegoldenrod",
                "forestgreen")
  ),
  verbatimTextOutput("result1")
)
server <- function(input, output, session) {
  output$result1 <- renderPrint({
    input$mycolor1
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### confirmSweetAlert

{{< highlight r >}}
confirmSweetAlert(session, inputId, title = "Are you sure ?", text = NULL, type = NULL, danger_mode = FALSE, btn_labels = c("Cancel", "Confirm"))
{{< /highlight >}}

#### confirmSweetAlertの説明

ユーザへの確認を行うポップアップを起動

#### confirmSweetAlertの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`title`**|アラートのタイトル|
|**`text`**|アラートのテキスト|
|**`type`**|アラートの型(`info`, `success`, `warning`, `error`)|
|**`danger_mode`**|論理値で危険モードをアクティベートするかどうかを指定(キャンセルボタンに焦点を当てます)。|
|**`btn_labels`**|ボタンのラベル|

#### confirmSweetAlertの使用例

{{< figure src="/ui-input/shinywidgets-confirmsweetalert.gif" alt="confirmSweetAlert" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Confirm sweet alert"),
  actionButton(
    inputId = "go",
    label = "Launch confirmation dialog"
  ),
  verbatimTextOutput(outputId = "res")
)
server <- function(input, output, session) {
  observeEvent(input$go, {
    confirmSweetAlert(
      session = session, inputId = "myconfirmation", type = "warning",
      title = "Want to confirm ?", danger_mode = TRUE
    )
  })
  output$res <- renderPrint(input$myconfirmation)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### dropdown

{{< highlight r >}}
dropdown(..., style = "default", status = "default", size = "md", icon = NULL, label = NULL, tooltip = FALSE, right = FALSE, up = FALSE, width = NULL, animate = FALSE)
{{< /highlight >}}

#### dropdownの説明

ドロップダウンメニューを生成

#### dropdownの引数

|名前|説明|
|:--|:--|
|**`...`**|ドロップダウンメニューに表示されるタグのリスト|
|**`style`**|`default`の場合、(`actionButton`のような)Bootstrapのボタンを使用します。他に`acutionBttn`を使用するなら、可能な値で引数の型を参照してください。|
|**`status`**|色を有効なBootstrapのステータス(`default`, `primary`, `info`, `success`, `warning`, `danger`)で指定します。|
|**`size`**|ボタンのサイズ(’default’, ’xs’, ’sm’, ’lg’)|
|**`icon`**|ボタン上に現れるアイコン|
|**`label`**|ボタン上に現れるラベル。`circle = TRUE`かつ`tooltip = TRUE`の場合、ラベルはツールチップ内で使用されます。|
|**`tooltip`**|ボタン上にツールチップを配置します。`tooltipOptions`でツールチップのカスタマイズが可能です。|
|**`right`**|論理値でドロップダウンメニューが右側に開くかどうかを指定します。|
|**`up`**|論理値で上部にドロップダウンメニューを表示するかどうかを指定します。|
|**`width`**|ドロップダウンメニューコンテンツの幅|
|**`animate`**|ドロップダウン上にアニメーションを追加します。論理値または`animateOptions`の結果を指定可能です。|

#### dropdownの詳細

この関数は`dropdownButton`に似ていますがBootstrapを使わないので、`pickerInput`を中に配置できます。さらにanimate.cssでドロップダウンの表示 / 非表示でのアニメーションを追加できます。

#### dropdownの使用例

{{< figure src="/ui-input/shinywidgets-dropdown.gif" alt="dropdown" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h2("pickerInput in dropdown"),
  br(),
  dropdown(
    tags$h3("List of Input"),
    pickerInput(inputId = 'xcol2',
                label = 'X Variable',
                choices = names(iris),
                options = list(`style` = "btn-info")),
    pickerInput(inputId = 'ycol2',
                label = 'Y Variable',
                choices = names(iris),
                selected = names(iris)[[2]],
                options = list(`style` = "btn-warning")),
    sliderInput(inputId = 'clusters2',
                label = 'Cluster count',
                value = 3,
                min = 1, max = 9),
    style = "unite", icon = icon("gear"),
    status = "danger", width = "300px",
    animate = animateOptions(
      enter = animations$fading_entrances$fadeInLeftBig,
      exit = animations$fading_exits$fadeOutRightBig
    )
  ),
  plotOutput(outputId = 'plot2')
)
server <- function(input, output, session) {
  selectedData2 <- reactive({
    iris[, c(input$xcol2, input$ycol2)]
  })
  clusters2 <- reactive({
    kmeans(selectedData2(), input$clusters2)
  })
  output$plot2 <- renderPlot({
    palette(c("#E41A1C", "#377EB8", "#4DAF4A",
              "#984EA3", "#FF7F00", "#FFFF33",
              "#A65628", "#F781BF", "#999999"))
    par(mar = c(5.1, 4.1, 0, 1))
    plot(selectedData2(),
         col = clusters2()$cluster,
         pch = 20, cex = 3)
    points(clusters2()$centers, pch = 4, cex = 4, lwd = 4)
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}


### dropdownButton

{{< highlight r >}}
dropdownButton(..., circle = TRUE, status = "default", size = "default", icon = NULL, label = NULL, tooltip = FALSE, right = FALSE, up = FALSE, width = NULL, inputId = NULL)
{{< /highlight >}}

#### dropdownButtonの説明

Bootstrapのドロップダウンメニューを生成

#### dropdownButtonの引数

|名前|説明|
|:--|:--|
|**`...`**|ドロップダウンメニューに表示されるタグのリスト|
|**`circle`**|丸ボタンを使用するかどうかを論理値で指定します。|
|**`status`**|ボタンにクラスを追加します。`info`, `primary`, `danger`, `warning`, `success`などのBootstrapのステータスを使用可能です。または、`status = 'myClass'`のように任意の文字列を指定することで、ボタンにクラス`btn-myClass`を持たせます。|
|**`size`**|ボタンのサイズ(’default’, ’xs’, ’sm’, ’lg’)|
|**`icon`**|ボタン上に現れるアイコン|
|**`label`**|ボタン上に現れるラベル。`circle = TRUE`かつ`tooltip = TRUE`の場合、ラベルはツールチップ内で使用されます。|
|**`tooltip`**|ボタン上にツールチップを配置します。`tooltipOptions`でツールチップのカスタマイズが可能です。|
|**`right`**|論理値でドロップダウンメニューが右側に開くかどうかを指定します。|
|**`up`**|論理値で上部にドロップダウンメニューを表示するかどうかを指定します。|
|**`width`**|ドロップダウンメニューコンテンツの幅|
|**`inputId`**|オプションでボタンのidを指定します。ボタンは`actionButton`のように動作し、idをサーバ側でドロップダウンメニューの切り替えに使用できます。|

#### dropdownButtonの使用例

{{< highlight r >}}
dropdownButton(
  "Your contents goes here ! You can pass several elements",
  circle = TRUE, status = "danger", icon = icon("gear"), width = "300px",
  tooltip = tooltipOptions(title = "Click to see inputs !")
)
{{< /highlight >}}


### inputSweetAlert

{{< highlight r >}}
inputSweetAlert(session, inputId, title = NULL, text = NULL, type = NULL, btn_labels = "Ok", placeholder = NULL)
{{< /highlight >}}

#### inputSweetAlertの説明

テキスト入力のポップアップを起動します。

#### inputSweetAlertの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`title`**|アラートのタイトル|
|**`text`**|アラートのテキスト|
|**`type`**|アラートの型(`info`, `success`, `warning`, `error`)|
|**`btn_labels`**|ボタンのラベル|
|**`placeholder`**|コントロールに何を入力すべきかユーザにヒントとして与える文字列|

#### inputSweetAlertの使用例

{{< figure src="/ui-input/shinywidgets-inputsweetalert.gif" alt="inputSweetAlert" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Confirm sweet alert"),
  actionButton(inputId = "go", label = "Launch input text dialog"),
  verbatimTextOutput(outputId = "res")
)
server <- function(input, output, session) {
  observeEvent(input$go, {
    inputSweetAlert(
      session = session, inputId = "mytext",
      title = "What's your name ?"
    )
  })
  output$res <- renderPrint(input$mytext)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### knobInput

{{< highlight r >}}
knobInput(inputId, label, value, min = 0, max = 100, step = 1, angleOffset = 0, angleArc = 360, cursor = FALSE, thickness = NULL, lineCap = c("default", "round"), displayInput = TRUE,
{{< /highlight >}}

{{< highlight r >}}
displayPrevious = FALSE, rotation = c("clockwise", "anticlockwise"), fgColor = NULL, inputColor = NULL, bgColor = NULL, readOnly = FALSE, skin = NULL, width = NULL, height = NULL)
{{< /highlight >}}

#### knobInputの説明

つまみの入力を生成します。

#### knobInputの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`value`**|初期値|
|**`min`**|指定可能な最小値。デフォルトは0。|
|**`max`**|指定可能な最大値。デフォルトは100。|
|**`step`**|選択可能なそれぞれの値の間隔を指定します。デフォルトは1です。|
|**`angleOffset`**|初期状態の角度を指定します。デフォルトは0です。|
|**`angleArc`**|弧の大きさを角度で指定します。デフォルトは360(度)です。|
|**`cursor`**|`TRUE`を指定すると表示モード"cursor"になります。`width`がピクセルで設定されていないと正しく動作しません。|
|**`thickness`**|ゲージの厚さを数値で指定|
|**`lineCap`**|ゲージのストロークの終端を`'default'`または`'round'`で指定|
|**`displayInput`**|つまみの中の入力を隠すかどうかを論理値で指定|
|**`displayPrevious`**|前の値を透明で表示するかどうかを論理値で指定|
|**`rotation`**|数列の方向を`'clockwise'`(時計回り)または`'anticlockwise'`(反時計回り)で指定|
|**`fgColor`**|前面の色|
|**`inputColor`**|入力した値(数値)の色|
|**`bgColor`**|背景の色|
|**`readOnly`**|つまみを無効にするかどうかを論理値で指定|
|**`skin`**|つまみのスキンを変えます。唯一指定可能なオプションは`'tron'`です。|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|
|**`height`**|入力の高さ。例えば、`400px`や`100%`のように指定します。|

#### knobInputの値

サーバ側での数値。

#### knobInputの使用例

{{< figure src="/ui-input/shinywidgets-knobinput.gif" alt="knobInputs" >}}

{{< highlight r >}}
ui <- fluidPage(
  knobInput(
    inputId = "myKnob",
    label = "Display previous:",
    value = 50,
    min = -100,
    displayPrevious = TRUE,
    fgColor = "#428BCA",
    inputColor = "#428BCA"
  ),
  verbatimTextOutput(outputId = "res")
)
server <- function(input, output, session) {
  output$res <- renderPrint(input$myKnob)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### materialSwitch

{{< highlight r >}}
materialSwitch(inputId, label = NULL, value = FALSE, status = "default", right = FALSE, inline = FALSE, width = NULL)
{{< /highlight >}}

#### materialSwitchの説明

マテリアルデザインのスイッチ入力で、オンとオフを切り替えるトグルスイッチを生成します。

#### materialSwitchの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|入力のラベル|
|**`value`**|`TRUE`または`FALSE`|
|**`status`**|色を有効なBootstrapのステータス(`default`, `primary`, `info`, `success`, `warning`, `danger`)で指定します。|
|**`right`**|ラベルを右側に表示するかどうかを論理値で指定します。デフォルトは`FALSE`です。|
|**`inline`**|ボタンをお互いに隣り合って配置したい場合に、入力をインラインに配置するかどうかを論理値で指定します。|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|

#### materialSwitchの値

UI定義に追加するスイッチコントロール

#### materialSwitchの使用例

{{< figure src="/ui-input/shinywidgets-materialswitch.png" alt="materialSwitch" >}}

{{< highlight r >}}
ui <- fluidPage(
  br(),
  materialSwitch(inputId = "somevalue", label = ""),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderText({ input$somevalue })
}
shinyApp(ui, server)
{{< /highlight >}}


### multiInput

{{< highlight r >}}
multiInput(inputId, label, choices = NULL, selected = NULL, options = NULL, width = NULL, choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

#### multiInputの説明

ユーザフレンドリな複数の属性付きのセレクトボックスの置き換えを生成します。

#### multiInputの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`choices`**|選択する値のリスト|
|**`selected`**|初期値で選択されている値|
|**`options`**|multiに渡すオプションのリスト。例えば、`enable_search = FALSE`で検索バーを無効にします|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|
|**`choiceNames`**|表示する名前のリスト|
|**`choiceValues`**|サーバで扱う値のリスト|

#### multiInputの値

複数選択のコントロール

#### multiInputの使用例

{{< figure src="/ui-input/shinywidgets-multiinput1.gif" alt="multiInput" >}}

{{< highlight r >}}
ui <- fluidPage(
  multiInput(
    inputId = "id", label = "Fruits :",
    choices = c("Banana", "Blueberry", "Cherry",
                "Coconut", "Grapefruit", "Kiwi",
                "Lemon", "Lime", "Mango", "Orange",
                "Papaya"),
    selected = "Banana", width = "350px"
  ),
  verbatimTextOutput(outputId = "res")
)
server <- function(input, output, session) {
  output$res <- renderPrint({
    input$id
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}

{{< figure src="/ui-input/shinywidgets-multiinput2.png" alt="multiInput with options" >}}

{{< highlight r >}}
# with options
ui <- fluidPage(
  multiInput(
    inputId = "id", label = "Fruits :",
    choices = c("Banana", "Blueberry", "Cherry",
                "Coconut", "Grapefruit", "Kiwi",
                "Lemon", "Lime", "Mango", "Orange",
                "Papaya"),
    selected = "Banana", width = "400px",
    options = list(
      enable_search = FALSE,
      non_selected_header = "Choose between:",
      selected_header = "You have selected:"
    )
  ),
  verbatimTextOutput(outputId = "res")
)
server <- function(input, output, session) {
  output$res <- renderPrint({
    input$id
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### panel

{{< highlight r >}}
panel(..., heading = NULL, footer = NULL, status = "default")
{{< /highlight >}}

#### panelの説明

基本的なボーダとパディングのあるパネル(ボックス)を生成します。。パネルのスタイルにはBootstrapのステータスを使用可能です。http://getbootstrap.com/components/#panels を参照してください。

#### panelの引数

|名前|説明|
|:--|:--|
|**`...`**|パネル内に含まれるUI要素|
|**`heading`**|プレーンなヘッダ内のパネルタイトル|
|**`footer`**|パネルのフッタ|
|**`status`**|文脈上の選択肢としてのBootstrapのステータス|

#### panelの値

UI定義

#### panelの使用例

{{< figure src="/ui-input/shinywidgets-panel.png" alt="panel" >}}

{{< highlight r >}}
ui <- fluidPage(
  # Default
  panel(
    "Content goes here",
    checkboxInput(inputId = "id1", label = "Label")
  ),
  # With header and footer
  panel(
    "Content goes here",
    checkboxInput(inputId = "id2", label = "Label"),
    heading = "My title",
    footer = "Something"
  ),
  # With status
  panel(
    "Content goes here",
    checkboxInput(inputId = "id3", label = "Label"),
    heading = "My title",
    status = "primary"
  )
)
server <- function(input, output, session) {
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}


### pickerInput

{{< highlight r >}}
pickerInput(inputId, label = NULL, choices, selected = NULL, multiple = FALSE, options = NULL, choicesOpt = NULL, width = NULL, inline = FALSE)
{{< /highlight >}}

#### pickerInputの説明

セレクトピッカ(https://silviomoreto.github.io/bootstrap-select/)を生成

#### pickerInputの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|スイッチに中央に表示するテキスト|
|**`choices`**|選択する値のリスト。リストの要素に名前がある場合、値ではなく名前がユーザに表示されます。|
|**`selected`**|初期値で選択されている値(`multiple = TRUE`の場合は、複数の値)。指定がない場合は、デフォルトで単独のリストの最初の値となり、複数のセレクトリストでは値がありません。|
|**`multiple`**|複数の項目を選択可能かどうかを論理値で指定|
|**`options`**|セレクトピッカをカスタマイズするオプション。https://silviomoreto.github.io/bootstrap-select/options/ を参照してください|
|**`choicesOpt`**|ドロップダウンメニュー内の選択肢のオプション|
|**`width`**|入力の幅。`auto`, `fit`, `100px`, `75%%`で指定します。|
|**`inline`**|ラベルとピッカを同じライン上に配置するかどうかを論理値で指定|

#### pickerInputの値

UI定義に追加する選択コントロール

#### pickerInputの使用例

{{< figure src="/ui-input/shinywidgets-pickerinput1.gif" alt="pickerInput" >}}

{{< highlight r >}}
# Simple example
ui <- fluidPage(
  pickerInput(inputId = "somevalue", label = "A label", choices = c("a", "b")),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderPrint({ input$somevalue })
}
shinyApp(ui, server)
{{< /highlight >}}

{{< figure src="/ui-input/shinywidgets-pickerinput2.gif" alt="pickerInput with actions box for selecting and deselecting all options" >}}

{{< highlight r >}}
# Add actions box for selecting
# deselecting all options
ui <- fluidPage(
  br(),
  pickerInput(
    inputId = "p1",
    label = "Select all option",
    choices = rownames(mtcars),
    multiple = TRUE,
    options = list(`actions-box` = TRUE)
  ),
  br(),
  pickerInput(
    inputId = "p2",
    label = "Select all option / custom text",
    choices = rownames(mtcars),
    multiple = TRUE,
    options = list(
      `actions-box` = TRUE,
      `deselect-all-text` = "None...",
      `select-all-text` = "Yeah, all !",
      `none-selected-text` = "zero"
    )
  )
)
server <- function(input, output, session) {
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}

{{< figure src="/ui-input/shinywidgets-pickerinput3.gif" alt="pickerInput with customized values displayed in the box" >}}

{{< highlight r >}}
# Customize the values displayed in the box
ui <- fluidPage(
  br(),
  pickerInput(
    inputId = "p1",
    label = "Default",
    multiple = TRUE,
    choices = rownames(mtcars),
    selected = rownames(mtcars)[1:5]
  ),
  br(),
  pickerInput(
    inputId = "p1b",
    label = "Default with | separator",
    multiple = TRUE,
    choices = rownames(mtcars),
    selected = rownames(mtcars)[1:5],
    options = list(`multiple-separator` = " | ")
  ),
  br(),
  pickerInput(
    inputId = "p2",
    label = "Static",
    multiple = TRUE,
    choices = rownames(mtcars),
    selected = rownames(mtcars)[1:5],
    options = list(`selected-text-format`= "static",
                   title = "Won't change")
  ),
  br(),
  pickerInput(
    inputId = "p3",
    label = "Count",
    multiple = TRUE,
    choices = rownames(mtcars),
    selected = rownames(mtcars)[1:5],
    options = list(`selected-text-format`= "count")
  ),
  br(),
  pickerInput(
    inputId = "p3",
    label = "Customize count",
    multiple = TRUE,
    choices = rownames(mtcars),
    selected = rownames(mtcars)[1:5],
    options = list(
      `selected-text-format`= "count",
      `count-selected-text` = "{0} models choosed (on a total of {1})"
    )
  )
)
server <- function(input, output, session) {
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}


### prettyCheckbox

{{< highlight r >}}
prettyCheckbox(inputId, label, value = FALSE, status = "default", shape = c("square", "curve", "round"), outline = FALSE, fill = FALSE, thick = FALSE, animation = NULL, icon = NULL, plain = FALSE, bigger = FALSE, width = NULL)
{{< /highlight >}}

#### prettyCheckboxの説明

論理値を指定するためのチェックボックスを生成

#### prettyCheckboxの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル|
|**`value`**|初期値を論理値(`TRUE`または`FALSE`)で指定|
|**`status`**|チェックボックスにクラスを追加します。`’info’`, `’primary’`, `’danger’`, `’warning’`, `’success’`のようなBootstrapのステータスが使用可能です。|
|**`shape`**|`square`, `curve`, `round`の間で指定するチェックボックスの形状|
|**`outline`**|チェックボックスの境界の色の有無を論理値で指定|
|**`fill`**|チェックボックスに色を塗るかどうかを論理値で指定|
|**`thick`**|チェックボックス内のコンテンツをより小さくするかどうかを論理値で指定|
|**`animation`**|チェックボックスがチェックされたときのアニメーションを追加します。値は`smooth`, `jelly`, `tada`, `rotate`, `pulse`から選択します。|
|**`icon`**|オプションでチェックボックス上に表示するアイコンを指定します。`icon`で生成されたアイコンである必要があります。|
|**`plain`**|チェックボックスがチェックされるときに境界を消すかどうかを論理値で指定|
|**`bigger`**|チェックボックスを拡大するかどうかを論理値で指定|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|

#### prettyCheckboxの値

サーバ側で`TRUE`または`FALSE`

#### prettyCheckboxの注記

異なるチェックボックスのデザインが自然なため、あるアニメーションでは、いくつかの引数の組み合わせが適用不可能です。pretty-checkboxの公式ページ(https:
//lokesh-coder.github.io/pretty-checkbox/)で例を見ることができます。

#### prettyCheckboxの使用例

{{< figure src="/ui-input/shinywidgets-prettycheckbox.gif" alt="prettyCheckbox" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Pretty checkbox"),
  br(),
  fluidRow(
    column(
      width = 4,
      prettyCheckbox(inputId = "checkbox1",
                     label = "Click me!"),
      verbatimTextOutput(outputId = "res1"),
      br(),
      prettyCheckbox(inputId = "checkbox4", label = "Click me!",
                     outline = TRUE,
                     plain = TRUE, icon = icon("thumbs-up")),
      verbatimTextOutput(outputId = "res4")
    ),
    column(
      width = 4,
      prettyCheckbox(inputId = "checkbox2",
                     label = "Click me!", thick = TRUE,
                     animation = "pulse", status = "info"),
      verbatimTextOutput(outputId = "res2"),
      br(),
      prettyCheckbox(inputId = "checkbox5",
                     label = "Click me!", icon = icon("check"),
                     animation = "tada", status = "default"),
      verbatimTextOutput(outputId = "res5")
    ),
    column(
      width = 4,
      prettyCheckbox(inputId = "checkbox3", label = "Click me!",
                     shape = "round", status = "danger",
                     fill = TRUE, value = TRUE),
      verbatimTextOutput(outputId = "res3")
    )
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$checkbox1)
  output$res2 <- renderPrint(input$checkbox2)
  output$res3 <- renderPrint(input$checkbox3)
  output$res4 <- renderPrint(input$checkbox4)
  output$res5 <- renderPrint(input$checkbox5)
}
shinyApp(ui, server)
{{< /highlight >}}


### prettyCheckboxGroup

{{< highlight r >}}
prettyCheckboxGroup(inputId, label, choices = NULL, selected = NULL, status = "default", shape = c("square", "curve", "round"), outline = FALSE, fill = FALSE, thick = FALSE, animation = NULL, icon = NULL, plain = FALSE, bigger = FALSE, inline = FALSE, width = NULL, choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

#### prettyCheckboxGroupの説明

複数の選択を独立にトグルで指定するpretty checkboxのグループを生成します。サーバでは、選択した値の文字ベクトルとして入力を受信します。

#### prettyCheckboxGroupの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル|
|**`choices`**|チェックボックスに表示する値のリスト。リストの要素に名前がある場合、値ではなく名前がユーザに表示されます。この引数が指定されると、`choiceNames`と`choiceValues`は指定できません。|
|**`selected`**|初期値として選択されている値|
|**`status`**|チェックボックスにクラスを追加します。`’info’`, `’primary’`, `’danger’`, `’warning’`, `’success’`のようなBootstrapのステータスが使用可能です。|
|**`shape`**|`square`, `curve`, `round`の間で指定するチェックボックスの形状|
|**`outline`**|チェックボックスの境界の色の有無を論理値で指定|
|**`fill`**|チェックボックスに色を塗るかどうかを論理値で指定|
|**`thick`**|チェックボックス内のコンテンツをより小さくするかどうかを論理値で指定|
|**`animation`**|チェックボックスがチェックされたときのアニメーションを追加します。値は`smooth`, `jelly`, `tada`, `rotate`, `pulse`から選択します。|
|**`icon`**|オプションでチェックボックス上に表示するアイコンを指定します。`icon`で生成されたアイコンである必要があります。|
|**`plain`**|チェックボックスがチェックされるときに境界を消すかどうかを論理値で指定|
|**`bigger`**|チェックボックスを拡大するかどうかを論理値で指定|
|**`inline`**|`TRUE`の場合、選択肢をインライン(すなわち水平)にレンダリングします。|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|
|**`choiceNames`**|ユーザに表示する名前のリスト|
|**`choiceValues`**|`choiceNames`に対応する値のリスト|

#### prettyCheckboxGroupの値

サーバ側で文字ベクトルまたは`NULL`。

#### prettyCheckboxGroupの使用例

{{< figure src="/ui-input/shinywidgets-prettycheckboxgroup.gif" alt="prettyCheckboxGroup" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Pretty checkbox group"),
  br(),
  fluidRow(
    column(
      width = 4,
      prettyCheckboxGroup(inputId = "checkgroup1",
                          label = "Click me!",
                          choices = c("Click me !", "Me !", "Or me !")),
      verbatimTextOutput(outputId = "res1"),
      br(),
      prettyCheckboxGroup(inputId = "checkgroup4", label = "Click me!",
                          choices = c("Click me !", "Me !", "Or me !"),
                          outline = TRUE,
                          plain = TRUE, icon = icon("thumbs-up")),
      verbatimTextOutput(outputId = "res4")
    ),
    column(
      width = 4,
      prettyCheckboxGroup(inputId = "checkgroup2",
                          label = "Click me!", thick = TRUE,
                          choices = c("Click me !", "Me !", "Or me !"),
                          animation = "pulse", status = "info"),
      verbatimTextOutput(outputId = "res2"),
      br(),
      prettyCheckboxGroup(inputId = "checkgroup5",
                          label = "Click me!", icon = icon("check"),
                          choices = c("Click me !", "Me !", "Or me !"),
                          animation = "tada", status = "default"),
      verbatimTextOutput(outputId = "res5")
    ),
    column(
      width = 4,
      prettyCheckboxGroup(inputId = "checkgroup3", label = "Click me!",
                          choices = c("Click me !", "Me !", "Or me !"),
                          shape = "round", status = "danger",
                          fill = TRUE, inline = TRUE),
      verbatimTextOutput(outputId = "res3")
    )
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$checkgroup1)
  output$res2 <- renderPrint(input$checkgroup2)
  output$res3 <- renderPrint(input$checkgroup3)
  output$res4 <- renderPrint(input$checkgroup4)
  output$res5 <- renderPrint(input$checkgroup5)
}
shinyApp(ui, server)
{{< /highlight >}}


