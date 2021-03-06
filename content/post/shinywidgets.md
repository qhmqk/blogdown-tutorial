---
title: "shinyWidgets"
author: "qhmqk"
date: 2018-03-27
categories: ["Shiny"]
tags: ["Packages"]
slug: "shinywidgets"
weight: 3
description: "RStudioによって開発されたパッケージshinyWidgetsの関数リファレンス。shinyWidgetsを用いることにより、さまざまなデザインのボタンやチェックボックス、ラジオボタンなどのUIを実装したスタイルシートを Shiny アプリケーションに適用することができます。"
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



### prettyRadioButtons

{{< highlight r >}}
prettyRadioButtons(inputId, label, choices = NULL, selected = NULL, status = "primary", shape = c("round", "square", "curve"), outline = FALSE, fill = FALSE, thick = FALSE, animation = NULL, icon = NULL, plain = FALSE, bigger = FALSE, inline = FALSE, width = NULL, choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

#### prettyRadioButtonsの説明

リストから項目を選択するpretty radio buttonの集合を生成します。

#### prettyRadioButtonsの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル|
|**`choices`**|選択する値のリスト。リストの要素に名前がある場合、値ではなく名前がユーザに表示されます。この引数が指定されると、`choiceNames`と`choiceValues`は指定できません。|
|**`seleted`**|初期値として選択されている値。指定されない場合はデフォルトで最初の値となります。|
|**`status`**|ラジオボタンにクラスを追加します。`’info’`, `’primary’`, `’danger’`, `’warning’`, `’success’`のようなBootstrapのステータスが使用可能です。|
|**`shape`**|`square`, `curve`, `round`の間で指定するラジオボタンの形状|
|**`outline`**|チェックボックスの境界の色の有無を論理値で指定|
|**`fill`**|ラジオボタンに色を塗るかどうかを論理値で指定|
|**`thick`**|ラジオボタン内のコンテンツをより小さくするかどうかを論理値で指定|
|**`animation`**|ラジオボタンがチェックされたときのアニメーションを追加します。値は`smooth`, `jelly`, `tada`, `rotate`, `pulse`から選択します。|
|**`icon`**|オプションでラジオボタン上に表示するアイコンを指定します。`icon`で生成されたアイコンである必要があります。|
|**`plain`**|チェックボックスがチェックされるときに境界を消すかどうかを論理値で指定|
|**`bigger`**|ラジオボタンを拡大するかどうかを論理値で指定|
|**`inline`**|`TRUE`の場合、選択肢をインライン(すなわち水平)にレンダリングします。|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|
|**`choiceNames`**|ユーザに表示する名前のリスト|
|**`choiceValues`**|`choiceNames`に対応する値のリスト|

#### prettyRadioButtonsの値

サーバ側で文字ベクトルまたは`NULL`。

#### prettyRadioButtonsの使用例

{{< figure src="/ui-input/shinywidgets-prettyradiobuttons.png" alt="prettyRadioButtons" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Pretty radio buttons"),
  br(),
  fluidRow(
    column(
      width = 4,
      prettyRadioButtons(inputId = "radio1",
                         label = "Click me!",
                         choices = c("Click me !", "Me !", "Or me !")),
      verbatimTextOutput(outputId = "res1"),
      br(),
      prettyRadioButtons(inputId = "radio4", label = "Click me!",
                         choices = c("Click me !", "Me !", "Or me !"),
                         outline = TRUE,
                         plain = TRUE, icon = icon("thumbs-up")),
      verbatimTextOutput(outputId = "res4")
    ),
    column(
      width = 4,
      prettyRadioButtons(inputId = "radio2",
                         label = "Click me!", thick = TRUE,
                         choices = c("Click me !", "Me !", "Or me !"),
                         animation = "pulse", status = "info"),
      verbatimTextOutput(outputId = "res2"),
      br(),
      prettyRadioButtons(inputId = "radio5",
                         label = "Click me!", icon = icon("check"),
                         choices = c("Click me !", "Me !", "Or me !"),
                         animation = "tada", status = "default"),
      verbatimTextOutput(outputId = "res5")
    ),
    column(
      width = 4,
      prettyRadioButtons(inputId = "radio3", label = "Click me!",
                         choices = c("Click me !", "Me !", "Or me !"),
                         shape = "round", status = "danger",
                         fill = TRUE, inline = TRUE),
      verbatimTextOutput(outputId = "res3")
    )
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$radio1)
  output$res2 <- renderPrint(input$radio2)
  output$res3 <- renderPrint(input$radio3)
  output$res4 <- renderPrint(input$radio4)
  output$res5 <- renderPrint(input$radio5)
}
shinyApp(ui, server)
{{< /highlight >}}



### prettySwitch

{{< highlight r >}}
prettySwitch(inputId, label, value = FALSE, status = "default", slim = FALSE, fill = FALSE, bigger = FALSE, width = NULL)
{{< /highlight >}}

#### prettySwitchの説明

チェックボックスを置き換えるトグル形式のpretty switchの入力を生成します。

#### prettySwitchの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`value`**|初期値を論理値(`TRUE`または`FALSE`)で指定|
|**`status`**|チェックボックスにクラスを追加します。`’info’`, `’primary’`, `’danger’`, `’warning’`, `’success’`のようなBootstrapのステータスが使用可能です。|
|**`slim`**|スイッチのスタイルを変えるかどうかを論理値で指定します。例を参照してください。|
|**`fill`**|スイッチのスタイルを変えるかどうかを論理値で指定します。例を参照してください。|
|**`bigger`**|チェックボックスを拡大するかどうかを論理値で指定|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|

#### prettySwitchの値

サーバ側で`TRUE`または`FALSE`

#### prettySwitchの注記

RStudioのビューワよりも、Chromeのようなブラウザの方がうまく表示できます。

#### prettySwitchの使用例

{{< figure src="/ui-input/shinywidgets-prettyswitch.gif" alt="prettySwitch" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Pretty switches"),
  br(),
  fluidRow(
    column(
      width = 4,
      prettySwitch(inputId = "switch1", label = "Default:"),
      verbatimTextOutput(outputId = "res1"),
      br(),
      prettySwitch(inputId = "switch4",
                   label = "Fill switch with status:",
                   fill = TRUE, status = "primary"),
      verbatimTextOutput(outputId = "res4")
    ),
    column(
      width = 4,
      prettySwitch(inputId = "switch2",
                   label = "Danger status:",
                   status = "danger"),
      verbatimTextOutput(outputId = "res2")
    ),
    column(
      width = 4,
      prettySwitch(inputId = "switch3",
                   label = "Slim switch:",
                   slim = TRUE),
      verbatimTextOutput(outputId = "res3")
    )
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$switch1)
  output$res2 <- renderPrint(input$switch2)
  output$res3 <- renderPrint(input$switch3)
  output$res4 <- renderPrint(input$switch4)
}
shinyApp(ui, server)
{{< /highlight >}}



### prettyToggle

{{< highlight r >}}
prettyToggle(inputId, label_on, label_off, icon_on = NULL, icon_off = NULL, value = FALSE, status_on = "success", status_off = "danger", shape = c("square", "curve", "round"), outline = FALSE, fill = FALSE, thick = FALSE, plain = FALSE, bigger = FALSE, width = NULL)
{{< /highlight >}}

#### prettyToggleの説明

チェックしたかどうかで表示を変えるpretty toggle入力を生成します。

#### prettyToggleの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label_on`**|値が`TRUE`のときにコントロールに表示するラベル|
|**`label_off`**|値が`FALSE`のときにコントロールに表示するラベル|
|**`icon_on`**|オプションで値が`TRUE`のときにチェックボックス上に表示するアイコンを指定します。`icon`で生成されたアイコンである必要があります。|
|**`icon_off`**|オプションで値が`FALSE`のときにチェックボックス上に表示するアイコンを指定します。`icon`で生成されたアイコンである必要があります。|
|**`value`**|初期値を論理値(`TRUE`または`FALSE`)で指定|
|**`status_on`**|値が`TRUE`のときのチェックボックスにクラスを追加します。`’info’`, `’primary’`, `’danger’`, `’warning’`, `’success’`のようなBootstrapのステータスが使用可能です。|
|**`status_off`**|値が`FALSE`のときのチェックボックスにクラスを追加します。`’info’`, `’primary’`, `’danger’`, `’warning’`, `’success’`のようなBootstrapのステータスが使用可能です。|
|**`shape`**|`square`, `curve`, `round`の間で指定するチェックボックスの形状|
|**`outline`**|チェックボックスの境界の色の有無を論理値で指定|
|**`fill`**|チェックボックスに色を塗るかどうかを論理値で指定|
|**`thick`**|チェックボックス内のコンテンツをより小さくするかどうかを論理値で指定|
|**`plain`**|チェックボックスがチェックされるときに境界を消すかどうかを論理値で指定|
|**`bigger`**|チェックボックスを拡大するかどうかを論理値で指定|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|

#### prettyToggleの値

サーバ側で`TRUE`または`FALSE`。

#### prettyToggleの使用例

{{< figure src="/ui-input/shinywidgets-prettytoggle.png" alt="prettyToggle" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Pretty toggles"),
  br(),
  fluidRow(
    column(
      width = 4,
      prettyToggle(inputId = "toggle1",
                   label_on = "Checked!",
                   label_off = "Unchecked..."),
      verbatimTextOutput(outputId = "res1"),
      br(),
      prettyToggle(inputId = "toggle4", label_on = "Yes!",
                   label_off = "No..", outline = TRUE,
                   plain = TRUE,
                   icon_on = icon("thumbs-up"),
                   icon_off = icon("thumbs-down")),
      verbatimTextOutput(outputId = "res4")
    ),
    column(
      width = 4,
      prettyToggle(inputId = "toggle2",
                   label_on = "Yes!", icon_on = icon("check"),
                   status_on = "info", status_off = "warning",
                   label_off = "No..", icon_off = icon("remove")),
      verbatimTextOutput(outputId = "res2")
    ),
    column(
      width = 4,
      prettyToggle(inputId = "toggle3", label_on = "Yes!",
                   label_off = "No..", shape = "round",
                   fill = TRUE, value = TRUE),
      verbatimTextOutput(outputId = "res3")
    )
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$toggle1)
  output$res2 <- renderPrint(input$toggle2)
  output$res3 <- renderPrint(input$toggle3)
  output$res4 <- renderPrint(input$toggle4)
}
shinyApp(ui, server)
{{< /highlight >}}



### progressBar

{{< highlight r >}}
progressBar(id, value, total = NULL, display_pct = FALSE, size = NULL, status = NULL, striped = FALSE, title = NULL)
{{< /highlight >}}

#### progressBarの説明

計算をフィードバックするために提供するプログレスバーを生成します。

#### progressBarの引数

|名前|説明|
|:--|:--|
|**`id`**|プログレスバーをアップデートするために用いられるid|
|**`value`**|0から100までの間のプログレスバーの値。100よりも大きくする場合は`total`を指定します。|
|**`total`**|`value`が100よりも大きい場合にパーセンテージを計算するために用いられる値。インジケータをプログレスバーの右上に表示させます。|
|**`display_pct`**|論理値でプログレスバー上にパーセンテージを表示するかどうかを指定|
|**`size`**|サイズを指定します。デフォルトは`NULL`で、値には` ’xxs’`, `’xs’`, `’sm’`を指定可能で、shinydashboardパッケージと一緒のときのみ有効です。|
|**`status`**|色を有効なBootstrapのステータス(`default`, `primary`, `info`, `success`, `warning`, `danger`)で指定します。|
|**`striped`**|論理値でストライプのエフェクトを追加するかどうかを指定|
|**`title`**|オプションで指定するタイトル文字列|

#### progressBarの値

UI定義に追加するプログレスバー。

#### progressBarの使用例

{{< figure src="/ui-input/shinywidgets-progressbar.gif" alt="progressBar" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$b("Default"), br(),
  progressBar(id = "pb1", value = 50),
  sliderInput(inputId = "up1", label = "Update", min = 0, max = 100, value = 50)
)
server <- function(input, output, session) {
  observeEvent(input$up1, {
    updateProgressBar(session = session, id = "pb1", value = input$up1)
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### progressSweetAlert

{{< highlight r >}}
progressSweetAlert(session, id, value, total = NULL, display_pct = FALSE, size = NULL, status = NULL, striped = FALSE, title = NULL)
{{< /highlight >}}

#### progressSweetAlertの説明

sweet aleart内のプログレスバー。

#### progressSweetAlertの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`id`**|プログレスバーをアップデートするために用いられるid|
|**`value`**|0から100までの間のプログレスバーの値。100よりも大きくする場合は`total`を指定します。|
|**`total`**|`value`が100よりも大きい場合にパーセンテージを計算するために用いられる値。インジケータをプログレスバーの右上に表示させます。|
|**`display_pct`**|論理値でプログレスバー上にパーセンテージを表示するかどうかを指定|
|**`size`**|サイズを指定します。デフォルトは`NULL`で、値には` ’xxs’`, `’xs’`, `’sm’`を指定可能で、shinydashboardパッケージと一緒のときのみ有効です。|
|**`status`**|色を有効なBootstrapのステータス(`default`, `primary`, `info`, `success`, `warning`, `danger`)で指定します。|
|**`striped`**|論理値でストライプのエフェクトを追加するかどうかを指定|
|**`title`**||

#### progressSweetAlertの使用例

{{< figure src="/ui-input/shinywidgets-progresssweetalert.gif" alt="progressSweetAlert" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Progress bar in Sweet Alert"),
  useSweetAlert(), # /!\ needed with 'progressSweetAlert'
  actionButton(
    inputId = "go",
    label = "Launch long calculation !"
  )
)
server <- function(input, output, session) {
  observeEvent(input$go, {
    progressSweetAlert(
      session = session, id = "myprogress",
      title = "Work in progress",
      display_pct = TRUE, value = 0
    )
    for (i in seq_len(50)) {
      Sys.sleep(0.1)
      updateProgressBar(
        session = session,
        id = "myprogress",
        value = i*2
      )
    }
    closeSweetAlert(session = session)
    sendSweetAlert(
      session = session,
      title =" Calculation completed !",
      type = "success"
    )
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### radioGroupButtons

{{< highlight r >}}
radioGroupButtons(inputId, label = NULL, choices = NULL, selected = NULL, status = "default", size = "normal", direction = "horizontal", justified = FALSE, individual = FALSE, checkIcon = list(), width = NULL, choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

#### radioGroupButtonsの説明

ラジオボタンのように動作するグループ化されたボタンを生成します。

#### radioGroupButtonsの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|入力のラベル|
|**`choices`**|選択する値のリスト。リストの要素に名前がある場合、値ではなく名前がユーザに表示されます。|
|**`selected`**|初期値で選択されている値|
|**`status`**|ボタンにクラスを追加します。`info`, `primary`, `danger`, `warning`, `success`などのBootstrapのステータスを使用可能です。または、`status = 'myClass'`のように任意の文字列を指定することで、ボタンにクラス`btn-myClass`を持たせます。|
|**`size`**|ボタンのサイズ(’default’, ’xs’, ’sm’, ’lg’)|
|**`direction`**|`horizontal`(水平)または`vertical`(垂直)を指定します。|
|**`justified`**|`TRUE`の場合、親の`<div>`の幅を埋めます。|
|**`individual`**|`TRUE`の場合、ボタンが分かれます。|
|**`checkIcon`**|少なくとも１つは空でない要素が含まれるリスト。ボタンがチェックされた場合に表示するアイコンを指定します。|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|
|**`choceNames`, `choiceValues`**|名前と値のリスト。それぞれアプリケーション内でユーザに各選択肢に対応するものが表示されます。このため、`choiceNames`と`choiceValues`は長さが同じである必要があります。|

#### radioGroupButtonsの値

UI定義に追加するボタングループコントロール。

#### radioGroupButtonsの使用例

{{< figure src="/ui-input/shinywidgets-radiogroupbuttons.png" alt="radioGroupButtons" >}}

{{< highlight r >}}
ui <- fluidPage(
  radioGroupButtons(inputId = "somevalue", choices = c("A", "B", "C")),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderText({ input$somevalue })
}
shinyApp(ui, server)
{{< /highlight >}}



### searchInput

{{< highlight r >}}
searchInput(inputId, label = NULL, value = "", placeholder = NULL, btnSearch = NULL, btnReset = NULL, width = NULL)
{{< /highlight >}}

#### searchInputの説明

エンターキーが押される、またはsearchボタンがクリックされたときがトリガーとなるテキスト入力。

#### searchInputの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`value`**|初期値|
|**`placeholder`**|コントロールに何を入力すべきかユーザにヒントとして与える文字列|
|**`btnSearch`**||
|**`btnReset`**||
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|

#### searchInputの注記

’search’と’reset’の2つのボタンは、`actionButton`のように動作します。それらの値をサーバ側で、`input$<INPUTID>_search`, `input$<INPUTID>_reset`として扱えます。

#### searchInputの使用例

{{< figure src="/ui-input/shinywidgets-searchinput.png" alt="searchInput" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Search Input"),
  br(),
  searchInput(
    inputId = "search", label = "Enter your text",
    placeholder = "A placeholder",
    btnSearch = icon("search"),
    btnReset = icon("remove"),
    width = "450px"
  ),
  br(),
  verbatimTextOutput(outputId = "res")
)
server <- function(input, output, session) {
  output$res <- renderPrint({
    input$search
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### sendSweetAlert

{{< highlight r >}}
sendSweetAlert(session, title = "Title", text = NULL, type = NULL, btn_labels = "Ok")
{{< /highlight >}}

#### sendSweetAlertの説明

サーバからメッセージを送信し、UIでsweet aleartを起動します。

#### sendSweetAlertの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`title`**|アラートのタイトル|
|**`tet`**|アラートのテキスト|
|**`type`**|アラートの型(`info`, `success`, `warning`, `error`)|
|**`btn_labels`**||

#### sendSweetAlertの使用例

{{< figure src="/ui-input/shinywidgets-sendsweetalert.gif" alt="sendSweetAlert" >}}

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Click the button"),
  actionButton(
    inputId = "success",
    label = "Launch a success sweet alert"
  ),
  actionButton(
    inputId = "error",
    label = "Launch an error sweet alert"
  )
)
server <- function(input, output, session) {
  observeEvent(input$success, {
    sendSweetAlert(
      session = session,
      title = "Success !!",
      text = "All in order",
      type = "success"
    )
  })
  observeEvent(input$error, {
    sendSweetAlert(
      session = session,
      title = "Error !!",
      text = "It's broken...",
      type = "error"
    )
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### shinyWidgetsGallery

{{< highlight r >}}
shinyWidgetsGallery()
{{< /highlight >}}

#### shinyWidgetsGalleryの説明

shinyWidgetsで利用可能なウィジェットのギャラリーを起動します。



### sliderTextInput

{{< highlight r >}}
sliderTextInput(inputId, label, choices, selected = NULL, animate = FALSE, grid = FALSE, hide_min_max = FALSE, from_fixed = FALSE, to_fixed = FALSE, from_min = NULL, from_max = NULL, to_min = NULL, to_max = NULL, force_edges = FALSE, width = NULL, pre = NULL, post = NULL, dragRange = TRUE)
{{< /highlight >}}

#### sliderTextInputの説明

数値の代わりに文字列があるスライダーのウィジェットを生成します。

#### sliderTextInputの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`choices`**|値を選択するための文字ベクトル|
|**`selected`**|初期値で選択されている値。`length > 1`の場合、幅のスライダーを生成します。|
|**`animate`**|`TRUE`の場合、デフォルトの設定でシンプルなアニメーションコントロールを表示。詳細は`sliderImput`を参照してください。|
|**`grid`**|論理値で針のマークを表示するかどうかを指定します。|
|**`hide_min_max`**|論理値で最大と最小のラベル表示を指定|
|**`from_fixed`**|論理値で左側のハンドルの位置固定を指定|
|**`to_fixed`**|論理値で右側のハンドルの位置固定を指定|
|**`from_min`**|左側のハンドルに最小値を設定|
|**`from_max`**|左側のハンドルに最大値を設定|
|**`to_min`**|右側のハンドルに最小値を設定|
|**`to_max`**|右側のハンドルに最大値を設定|
|**`force_edges`**|論理値でスライダーが常にコンテナ内に置くかどうかを指定|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|
|**`pre`**|値の前に置くprefixの文字列|
|**`post`**|値の後に置くsuffixの文字列|
|**`dragRange`**|`sliderInput`の同じ引数を参照してください。|

#### sliderTextInputの値

サーバ側で扱う値は文字ベクトルです。

#### sliderTextInputの使用例

{{< figure src="/ui-input/shinywidgets-slidertextinput.png" alt="sliderTextInput" >}}

{{< highlight r >}}
ui <- fluidPage(
  br(),
  sliderTextInput(
    inputId = "mySliderText",
    label = "Month range slider:",
    choices = month.name,
    selected = month.name[c(4, 7)]
  ),
  verbatimTextOutput(outputId = "result")
)
server <- function(input, output, session) {
  output$result <- renderPrint(str(input$mySliderText))
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### spectrumInput

{{< highlight r >}}
spectrumInput(inputId, label, choices = NULL, selected = NULL, flat = FALSE, options = list(), width = NULL)
{{< /highlight >}}

#### spectrumInputの説明

パレット内で色を選択するウィジェットを生成します。必要に応じてオプションを追加することができます。

#### spectrumInputの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`choices`**|メニューに表示する色のリスト|
|**`selected`**|初期値で選択されている値|
|**`flat`**|メニューをインラインで表示するかどうかを論理値で指定|
|**`options`**|スペクトルに渡す追加のオプション。指定可能な値は https://bgrins.github.io/spectrum/#options を参照してください。|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|

#### spectrumInputの値

サーバ側で16進フォーマットの選択された色。

#### spectrumInputの使用例

{{< figure src="/ui-input/shinywidgets-spectruminput.gif" alt="spectrumInput" >}}

{{< highlight r >}}
library("RColorBrewer")
ui <- fluidPage(
  tags$h1("Spectrum color picker"),
  br(),
  spectrumInput(
    inputId = "myColor",
    label = "Pick a color:",
    choices = list(
      list('black', 'white', 'blanchedalmond', 'steelblue', 'forestgreen'),
      as.list(brewer.pal(n = 9, name = "Blues")),
      as.list(brewer.pal(n = 9, name = "Greens")),
      as.list(brewer.pal(n = 11, name = "Spectral")),
      as.list(brewer.pal(n = 8, name = "Dark2"))
    ),
    options = list(`toggle-palette-more-text` = "Show more")
  ),
  verbatimTextOutput(outputId = "res")
)
server <- function(input, output, session) {
  output$res <- renderPrint(input$myColor)
}
shinyApp(ui, server)
{{< /highlight >}}



### switchInput

{{< highlight r >}}
switchInput(inputId, label = NULL, value = FALSE, onLabel = "ON", offLabel = "OFF", onStatus = NULL, offStatus = NULL, size = "default", labelWidth = "auto", handleWidth = "auto", disabled = FALSE, inline = FALSE, width = NULL)
{{< /highlight >}}

#### switchInputの説明

Bootstrapのトグルスイッチ入力を生成します。

#### switchInputの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|スイッチに中央に表示するテキスト|
|**`value`**|初期値を論理値(`TRUE`または`FALSE`)で指定|
|**`onLabel`**|スイッチの左側(`TRUE`)のテキスト|
|**`offLabel`**|スイッチの右側(`FALSE`)のテキスト|
|**`onStatus`**|スイッチの左側(`TRUE`)の色のBootstrapステータス|
|**`offStatus`**|スイッチの右側(`FALSE`)の色のBootstrapステータス|
|**`size`**|ボタンのサイズ(’default’, ’mini’, ’small’, ’normal’, ’large’)|
|**`labelWidth`**|中央のハンドルの幅をピクセルで指定|
|**`handleWidth`**|左側と右側の幅をピクセルで指定|
|**`disabled`**|トグルスイッチを無効にした状態で表示するかどうかを論理値で指定|
|**`inline`**|トグルスイッチをインラインで表示するかどうかを論理値で指定|
|**`width`**|入力の幅。例えば、`400px`や`100%`のように指定します。|

#### switchInputの値

UI定義に追加するスイッチコントロール。

#### switchInputの注記

すべてのオプションは http://bootstrapswitch.com/options.html で記述されています。

#### switchInputの使用例

{{< figure src="/ui-input/shinywidgets-switchinput.gif" alt="switchInput" >}}

{{< highlight r >}}
ui <- fluidPage(
  switchInput(inputId = "somevalue"),
  verbatimTextOutput("value")
)
server <- function(input, output) {
  output$value <- renderPrint({ input$somevalue })
}
shinyApp(ui, server)
{{< /highlight >}}



### textInputAddon

{{< highlight r >}}
textInputAddon(inputId, label, value = "", placeholder = NULL, addon, width = NULL)
{{< /highlight >}}

#### textInputAddonの説明

add-on付きのテキスト入力領域を生成します。

#### textInputAddonの引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために用いられる入力のスロット|
|**`label`**|コントロールに表示するラベル。`NULL`ならラベル無しとなります。|
|**`value`**|初期値|
|**`placeholder`**|コントロールに何を入力すべきかユーザにヒントとして与える文字列|
|**`addon`**|`icon`で生成するアイコンタグ|
|**`width`**|入力の幅。`auto`, `fit`, `100px`, `750%`で指定します。|

#### textInputAddonの値

UI定義に追加するテキスト入力コントロール。

#### textInputAddonの使用例

{{< figure src="/ui-input/shinywidgets-textinputaddon.png" alt="textInputAddon" >}}

{{< highlight r >}}
ui <- fluidPage(
  textInputAddon(inputId = "id", label = "Label", placeholder = "Username", addon = icon("at")),
  verbatimTextOutput(outputId = "out")
)
server <- function(input, output) {
  output$out <- renderPrint({
    input$id
  })
}
shinyApp(ui, server)
{{< /highlight >}}



### toggleDropdownButton 

{{< highlight r >}}
toggleDropdownButton(inputId)
{{< /highlight >}}

#### toggleDropdownButtonの説明

サーバ側でドロップダウンメニューを開く、または閉じます。

#### toggleDropdownButtonの引数

|名前|説明|
|:--|:--|
|**`inputId`**|トグルへのドロップダウンのID|


### tooltipOptions

{{< highlight r >}}
tooltipOptions(placement = "right", title = "Params", html = FALSE)
{{< /highlight >}}

#### tooltipOptionsの説明

ドロップダウンメニューボタンのツールチップオプションのリスト。

#### tooltipOptionsの引数

|名前|説明|
|:--|:--|
|**`placement`**|ツールチップの配置(`right`, `top`, `bottom`, `left`)を指定|
|**`title`**|ツールチップのテキスト|
|**`html`**|ツールチップ内でHTMLタグを使用できるようにするかどうかを論理値で指定|



### updateAwesomeCheckbox

{{< highlight r >}}
updateAwesomeCheckbox(session, inputId, label = NULL, value = NULL)
{{< /highlight >}}

#### updateAwesomeCheckboxの説明

クライアント上でasesome checkbox入力の値を変更します。

#### updateAwesomeCheckboxの引数

|名前|説明|
|:--|:--|
|**`session`**|標準的なShinyのsession|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力オブジェクトに設定するラベル|
|**`value`**|入力オブジェクトに設定する値|

#### updateAwesomeCheckboxの使用例

{{< figure src="/ui-input/shinywidgets-updateawesomecheckbox.gif" alt="updateAwesomeCheckbox" >}}

{{< highlight r >}}
ui <- fluidPage(
  awesomeCheckbox(
    inputId = "somevalue",
    label = "My label",
    value = FALSE
  ),
  verbatimTextOutput(outputId = "res"),
  actionButton(inputId = "updatevalue", label = "Toggle value"),
  textInput(inputId = "updatelabel", label = "Update label")
)
server <- function(input, output, session) {
  output$res <- renderPrint({
    input$somevalue
  })
  observeEvent(input$updatevalue, {
    updateAwesomeCheckbox(
      session = session, inputId = "somevalue",
      value = as.logical(input$updatevalue %%2)
    )
  })
  observeEvent(input$updatelabel, {
    updateAwesomeCheckbox(
      session = session, inputId = "somevalue",
      label = input$updatelabel
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### updateAwesomeCheckboxGroup

{{< highlight r >}}
updateAwesomeCheckboxGroup(session, inputId, label = NULL, choices = NULL, selected = NULL, inline = FALSE, status = "primary")
{{< /highlight >}}

#### updateAwesomeCheckboxGroupの説明

クライアント上で`awesomeCheckboxGroup`の値を変更します。

#### updateAwesomeCheckboxGroupの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力のラベル|
|**`choices`**|チェックボックスに表示する値のリスト|
|**`selected`**|初期値として選択されている値|
|**`inline`**|`TRUE`の場合、選択肢をインライン(すなわち水平)にレンダリングします。|
|**`stats`**|ボタンの色|

#### updateAwesomeCheckboxGroupの使用例

{{< highlight r >}}
ui <- fluidPage(
  awesomeCheckboxGroup(
    inputId = "somevalue",
    choices = c("A", "B", "C"),
    label = "My label"
  ),
  verbatimTextOutput(outputId = "res"),
  actionButton(inputId = "updatechoices", label = "Random choices"),
  textInput(inputId = "updatelabel", label = "Update label")
)
server <- function(input, output, session) {
  output$res <- renderPrint({
    input$somevalue
  })
  observeEvent(input$updatechoices, {
    updateAwesomeCheckboxGroup(
      session = session, inputId = "somevalue",
      choices = sample(letters, sample(2:6))
    )
  })
  observeEvent(input$updatelabel, {
    updateAwesomeCheckboxGroup(
      session = session, inputId = "somevalue",
      label = input$updatelabel
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### updateAwesomeRadio

{{< highlight r >}}
updateAwesomeRadio(session, inputId, label = NULL, choices = NULL, selected = NULL, inline = FALSE, status = "primary", checkbox = FALSE)
{{< /highlight >}}

#### updateAwesomeRadioの説明

クライアント上で`awesomeRadio`のラジオボタン入力の値を変更します。

#### updateAwesomeRadioの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力のラベル|
|**`choices`**|選択する値のリスト。リストの要素に名前がある場合、値ではなく名前がユーザに表示されます。|
|**`selected`**|初期値で選択されている値|
|**`inline`**|`TRUE`の場合、選択肢をインライン(すなわち水平)にレンダリングします。|
|**`status`**|ボタンの色|
|**`checkbox`**|チェックボックスのスタイル|

#### updateAwesomeRadioの使用例

{{< highlight r >}}
ui <- fluidPage(
  awesomeRadio(
    inputId = "somevalue",
    choices = c("A", "B", "C"),
    label = "My label"
  ),
  verbatimTextOutput(outputId = "res"),
  actionButton(inputId = "updatechoices", label = "Random choices"),
  textInput(inputId = "updatelabel", label = "Update label")
)
server <- function(input, output, session) {
  output$res <- renderPrint({
    input$somevalue
  })
  observeEvent(input$updatechoices, {
    updateAwesomeRadio(
      session = session, inputId = "somevalue",
      choices = sample(letters, sample(2:6))
    )
  })
  observeEvent(input$updatelabel, {
    updateAwesomeRadio(
      session = session, inputId = "somevalue",
      label = input$updatelabel
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### updateCheckboxGroupButtons

{{< highlight r >}}
updateCheckboxGroupButtons(session, inputId, label = NULL, choices = NULL, selected = NULL, status = "default", size = "normal", checkIcon = list(), choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

#### updateCheckboxGroupButtonsの説明

クライアント上で`checkboxGroupButtons`入力の値を変更します。

#### updateCheckboxGroupButtonsの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|設定するラベル|
|**`choices`**|入力の新しい選択肢|
|**`selected`**|選択されている値|
|**`status`**|`choices`が`NULL`でない場合にのみ用いられるステータス|
|**`size`**|`choices`が`NULL`でない場合にのみ用いられるサイズ|
|**`choeckIcon`**|`choices`が`NULL`でない場合にのみ用いられるアイコン|
|**`choiceNames`, `choiceValues`**|名前と値のリスト。`choices`の代わりに用います。|

#### updateCheckboxGroupButtonsの使用例

{{< highlight r >}}
# Example 1 ----
ui <- fluidPage(
  radioButtons(inputId = "up", label = "Update button :", choices = c("All", "None")),
  checkboxGroupButtons(
    inputId = "btn", label = "Power :",
    choices = c("Nuclear", "Hydro", "Solar", "Wind"),
    selected = "Hydro"
  ),
  verbatimTextOutput(outputId = "res")
)
server <- function(input,output, session){
  observeEvent(input$up, {
    if (input$up == "All"){
      updateCheckboxGroupButtons(session, "btn", selected = c("Nuclear", "Hydro", "Solar", "Wind"))
    } else {
      updateCheckboxGroupButtons(session, "btn", selected = character(0))
    }
  }, ignoreInit = TRUE)
  output$res <- renderPrint({
    input$btn
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}

{{< highlight r >}}
# Example 2 ----
ui <- fluidPage(
  checkboxGroupButtons(
    inputId = "somevalue",
    choices = c("A", "B", "C"),
    label = "My label"
  ),
  verbatimTextOutput(outputId = "res"),
  actionButton(inputId = "updatechoices", label = "Random choices"),
  pickerInput(
    inputId = "updateselected", label = "Update selected:",
    choices = c("A", "B", "C"), multiple = TRUE
  ),
  textInput(inputId = "updatelabel", label = "Update label")
)
server <- function(input, output, session) {
  output$res <- renderPrint({
    input$somevalue
  })
  observeEvent(input$updatechoices, {
    newchoices <- sample(letters, sample(2:6))
    updateCheckboxGroupButtons(
      session = session, inputId = "somevalue",
      choices = newchoices
    )
    updatePickerInput(
      session = session, inputId = "updateselected",
      choices = newchoices
    )
  })
  observeEvent(input$updateselected, {
    updateCheckboxGroupButtons(
      session = session, inputId = "somevalue",
      selected = input$updateselected
    )
  }, ignoreNULL = TRUE, ignoreInit = TRUE)
  observeEvent(input$updatelabel, {
    updateCheckboxGroupButtons(
      session = session, inputId = "somevalue",
      label = input$updatelabel
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}


### updateKnobInput

{{< highlight r >}}
updateKnobInput(session, inputId, label = NULL, value = NULL)
{{< /highlight >}}

#### updateKnobInputの説明

クライアント上でつまみの入力`knobInput`の値を変更します。

#### updateKnobInputの引数

|名前|説明|
|:--|:--|
|**`session`**|標準的なShinyのsession|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力オブジェクトに設定するラベル|
|**`value`**|入力オブジェクトに設定する値|

#### updateKnobInputの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("knob update examples"),
  br(),
  fluidRow(
    column(
      width = 6,
      knobInput(
        inputId = "knob1", label = "Update value:",
        value = 75, angleOffset = 90, lineCap = "round"
      ),
      verbatimTextOutput(outputId = "res1"),
      sliderInput(
        inputId = "upknob1", label = "Update knob:",
        min = 0, max = 100, value = 75
      )
    ),
    column(
      width = 6,
      knobInput(
        inputId = "knob2", label = "Update label:",
        value = 50, angleOffset = -125, angleArc = 250
      ),
      verbatimTextOutput(outputId = "res2"),
      textInput(inputId = "upknob2", label = "Update label:")
    )
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$knob1)
  observeEvent(input$upknob1, {
    updateKnobInput(
      session = session,
      inputId = "knob1",
      value = input$upknob1
    )
  }, ignoreInit = TRUE)
  output$res2 <- renderPrint(input$knob2)
  observeEvent(input$upknob2, {
    updateKnobInput(
      session = session,
      inputId = "knob2",
      label = input$upknob2
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### updateMaterialSwitch

{{< highlight r >}}
updateMaterialSwitch(session, inputId, value = NULL)
{{< /highlight >}}

#### updateMaterialSwitchの説明

クライアント上で`materialSwitch`入力の値を変更します。

#### updateMaterialSwitchの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`value`**|入力オブジェクトに設定する値|


### updatePickerInput

{{< highlight r >}}
updatePickerInput(session, inputId, label = NULL, selected = NULL, choices = NULL, choicesOpt = NULL)
{{< /highlight >}}

#### updatePickerInputの説明

クライアント上で`pickerInput`入力の値を変更します。

#### updatePickerInputの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|スイッチに中央に表示するテキスト|
|**`selected`**|初期値で選択されている値(`multiple = TRUE`の場合は、複数の値)。指定がない場合は、デフォルトで単独のリストの最初の値となり、複数のセレクトリストでは値がありません。|
|**`choices`**|選択する値のリスト。リストの要素に名前がある場合、値ではなく名前がユーザに表示されます。|
|**`choicesOpt`**|ドロップダウンメニュー内の選択肢のオプション|

#### updatePickerInputの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h2("Update pickerInput"),
  fluidRow(
    column(
      width = 5, offset = 1,
      pickerInput(
        inputId = "p1",
        label = "classic update",
        choices = rownames(mtcars)
      )
    ),
    column(
      width = 5,
      pickerInput(
        inputId = "p2",
        label = "disabled update",
        choices = rownames(mtcars)
      )
    )
  ),
  fluidRow(
    column(
      width = 10, offset = 1,
      sliderInput(
        inputId = "up",
        label = "Select between models with mpg greater than :",
        width = "50%",
        min = min(mtcars$mpg),
        max = max(mtcars$mpg),
        value = min(mtcars$mpg),
        step = 0.1
      )
    )
  )
)
server <- function(input, output, session) {
  observeEvent(input$up, {
    mtcars2 <- mtcars[mtcars$mpg >= input$up, ]
    # Method 1
    updatePickerInput(session = session, inputId = "p1",
                      choices = rownames(mtcars2))
    # Method 2
    disabled_choices <- !rownames(mtcars) %in% rownames(mtcars2)
    updatePickerInput(
      session = session, inputId = "p2",
      choices = rownames(mtcars),
      choicesOpt = list(
        disabled = disabled_choices,
        style = ifelse(disabled_choices,
                       yes = "color: rgba(119, 119, 119, 0.5);",
                       no = "")
      )
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### updatePrettyCheckbox

{{< highlight r >}}
updatePrettyCheckbox(session, inputId, label = NULL, value = NULL)
{{< /highlight >}}

#### updatePrettyCheckboxの説明

クライアント上で`prettyCheckbox`の値を変更します。

#### updatePrettyCheckboxの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力オブジェクトに設定するラベル|
|**`value`**|入力オブジェクトに設定する値|

#### updatePrettyCheckboxの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Pretty checkbox update value"),
  br(),
  prettyCheckbox(inputId = "checkbox1",
                 label = "Update me!",
                 shape = "curve", thick = TRUE, outline = TRUE),
  verbatimTextOutput(outputId = "res1"),
  radioButtons(
    inputId = "update", label = "Value to set:",
    choices = c("FALSE", "TRUE")
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$checkbox1)
  observeEvent(input$update, {
    updatePrettyToggle(session = session,
                       inputId = "checkbox1",
                       value = as.logical(input$update))
  })
}
shinyApp(ui, server)
{{< /highlight >}}



### updatePrettyCheckboxGroup

{{< highlight r >}}
updatePrettyCheckboxGroup(session, inputId, label = NULL, choices = NULL, selected = NULL, inline = FALSE, choiceNames = NULL, choiceValues = NULL, prettyOptions = list())
{{< /highlight >}}

#### updatePrettyCheckboxGroupの説明

クライアント上で`prettyCheckboxGroup`の値を変更します。

#### updatePrettyCheckboxGroupの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力オブジェクトに設定するラベル|
|**`choices`**|入力オブジェクトに設定する選択肢。アップデートによりパラメータはリセットされます。|
|**`selected`**|入力オブジェクトに設定する値|
|**`inline`**|`TRUE`の場合、選択肢をインライン(すなわち水平)にレンダリングします。|
|**`choiceNames`**|入力オブジェクトに設定する選択肢の名前|
|**`choiceValues`**|入力オブジェクトに設定する選択肢の値|
|**`prettyOptions`**|チェックボックスのスタイルを変更するために`prettyCheckboxGroup`に渡される引数|

#### updatePrettyCheckboxGroupの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Update pretty checkbox group"),
  br(),
  fluidRow(
    column(
      width = 6,
      prettyCheckboxGroup(inputId = "checkgroup1",
                          label = "Update my value!",
                          choices = month.name[1:4],
                          status = "danger",
                          icon = icon("remove")),
      verbatimTextOutput(outputId = "res1"),
      br(),
      checkboxGroupInput(
        inputId = "update1", label = "Update value :",
        choices = month.name[1:4], inline = TRUE
      )
    ),
    column(
      width = 6,
      prettyCheckboxGroup(inputId = "checkgroup2",
                          label = "Update my choices!", thick = TRUE,
                          choices = month.name[1:4],
                          animation = "pulse", status = "info"),
      verbatimTextOutput(outputId = "res2"),
      br(),
      actionButton(inputId = "update2", label = "Update choices !")
    )
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$checkgroup1)
  observeEvent(input$update1, {
    if (is.null(input$update1)) {
      selected_ <- character(0) # no choice selected
    } else {
      selected_ <- input$update1
    }
    updatePrettyCheckboxGroup(session = session, inputId = "checkgroup1", selected = selected_)
  }, ignoreNULL = FALSE)
  output$res2 <- renderPrint(input$checkgroup2)
  observeEvent(input$update2, {
    updatePrettyCheckboxGroup(
      session = session, inputId = "checkgroup2",
      choices = sample(month.name, 4), prettyOptions = list(animation = "pulse", status = "info")
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui, server)
{{< /highlight >}}



### updatePrettyRadioButtons

{{< highlight r >}}
updatePrettyRadioButtons(session, inputId, label = NULL, choices = NULL, selected = NULL, inline = FALSE, choiceNames = NULL, choiceValues = NULL, prettyOptions = list())
{{< /highlight >}}

#### updatePrettyRadioButtonsの説明

クライアント上で`prettyRadioButtons`の値を変更します。

#### updatePrettyRadioButtonsの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力オブジェクトに設定するラベル|
|**`choices`**入力オブジェクトに設定する選択肢。アップデートによりパラメータはリセットされます。|
|**`selected`**|入力オブジェクトに設定する値|
|**`inline`**|`TRUE`の場合、選択肢をインライン(すなわち水平)にレンダリングします。|
|**`choiceNames`**|入力オブジェクトに設定する選択肢の名前|
|**`choiceValues`**|入力オブジェクトに設定する選択肢の値|
|**`prettyOptions`**|ラジオボタンのスタイルを変更するために`prettyRadioButtons`に渡される引数|

#### updatePrettyRadioButtonsの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Update pretty radio buttons"),
  br(),
  fluidRow(
    column(
      width = 6,
      prettyRadioButtons(inputId = "radio1",
                         label = "Update my value!",
                         choices = month.name[1:4],
                         status = "danger",
                         icon = icon("remove")),
      verbatimTextOutput(outputId = "res1"),
      br(),
      radioButtons(
        inputId = "update1", label = "Update value :",
        choices = month.name[1:4], inline = TRUE
      )
    ),
    column(
      width = 6,
      prettyRadioButtons(inputId = "radio2",
                         label = "Update my choices!", thick = TRUE,
                         choices = month.name[1:4],
                         animation = "pulse", status = "info"),
      verbatimTextOutput(outputId = "res2"),
      br(),
      actionButton(inputId = "update2", label = "Update choices !")
    )
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$radio1)
  observeEvent(input$update1, {
    updatePrettyRadioButtons(
      session = session,
      inputId = "radio1",
      selected = input$update1
    )
  }, ignoreNULL = FALSE)
  output$res2 <- renderPrint(input$radio2)
  observeEvent(input$update2, {
    updatePrettyRadioButtons(
      session = session, inputId = "radio2",
      choices = sample(month.name, 4),
      prettyOptions = list(animation = "pulse",
                           status = "info",
                           shape = "round")
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui, server)
{{< /highlight >}}



### updatePrettySwitch

{{< highlight r >}}
updatePrettySwitch(session, inputId, label = NULL, value = NULL)
{{< /highlight >}}

#### updatePrettySwitchの説明

クライアント上で`prettySwitch`の値を変更します。

#### updatePrettySwitchの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力オブジェクトに設定するラベル|
|**`value`**|入力オブジェクトに設定する値|

#### updatePrettySwitchの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Pretty switch update value"),
  br(),
  prettySwitch(inputId = "switch1", label = "Update me !"),
  verbatimTextOutput(outputId = "res1"),
  radioButtons(
    inputId = "update", label = "Value to set:",
    choices = c("FALSE", "TRUE")
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$switch1)
  observeEvent(input$update, {
    updatePrettySwitch(session = session, inputId = "switch1",
                       value = as.logical(input$update))
  })
}
shinyApp(ui, server)
{{< /highlight >}}



### updatePrettyToggle

{{< highlight r >}}
updatePrettyToggle(session, inputId, label = NULL, value = NULL)
{{< /highlight >}}

#### updatePrettyToggleの説明

クライアント上で`prettyToggle`の値を変更します。

#### updatePrettyToggleの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|入力オブジェクトに設定するラベル|
|**`value`**|入力オブジェクトに設定する値|

#### updatePrettyToggleの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Pretty toggle update value"),
  br(),
  prettyToggle(inputId = "toggle1",
               label_on = "Checked!",
               label_off = "Unchecked..."),
  verbatimTextOutput(outputId = "res1"),
  radioButtons(
    inputId = "update", label = "Value to set:",
    choices = c("FALSE", "TRUE")
  )
)
server <- function(input, output, session) {
  output$res1 <- renderPrint(input$toggle1)
  observeEvent(input$update, {
    updatePrettyToggle(session = session,
                       inputId = "toggle1",
                       value = as.logical(input$update))
  })
}
shinyApp(ui, server)
{{< /highlight >}}



### updateProgressBar

{{< highlight r >}}
updateProgressBar(session, id, value, total = NULL, status = NULL)
{{< /highlight >}}

#### updateProgressBarの説明

クライアント上でプログレスバーの値を変更します。

#### updateProgressBarの引数

|名前|説明|
|:--|:--|
|**`session`**`shinyServer`に与えられた関数に渡されるセッションオブジェクト||
|**`id`**|プログレスバーを更新するためのid|
|**`value`**|0から100までの間のプログレスバーの値。100よりも大きくする場合は`total`を指定します。|
|**`total`**|`value`が100よりも大きい場合にパーセンテージを計算するために用いられる値|
|**`status`**|色|



### updateRadioGroupButtons

{{< highlight r >}}
updateRadioGroupButtons(session, inputId, label = NULL, choices = NULL, selected = NULL, status = "default", size = "normal", checkIcon = list(), choiceNames = NULL, choiceValues = NULL)
{{< /highlight >}}

#### updateRadioGroupButtonsの説明

クライアント上で`radioGroupButtons`の値を変更します。

#### updateRadioGroupButtonsの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|設定するラベル|
|**`choices`**|入力の新しい選択肢|
|**`selected`**|選択されている値|
|**`status`**|`choices`が`NULL`でない場合にのみ用いられるステータス|
|**`size`**|`choices`が`NULL`でない場合にのみ用いられるサイズ|
|**`checkIcon`**|`choices`が`NULL`でない場合にのみ用いられるアイコン|
|**`choiceNames`, `choiceValues`**|名前と値のリスト。`choices`の代わりに用います。|

#### updateRadioGroupButtonsの使用例

{{< highlight r >}}
ui <- fluidPage(
  radioGroupButtons(
    inputId = "somevalue",
    choices = c("A", "B", "C"),
    label = "My label"
  ),
  verbatimTextOutput(outputId = "res"),
  actionButton(inputId = "updatechoices", label = "Random choices"),
  pickerInput(
    inputId = "updateselected", label = "Update selected:",
    choices = c("A", "B", "C"), multiple = FALSE
  ),
  textInput(inputId = "updatelabel", label = "Update label")
)
server <- function(input, output, session) {
  output$res <- renderPrint({
    input$somevalue
  })
  observeEvent(input$updatechoices, {
    newchoices <- sample(letters, sample(2:6))
    updateRadioGroupButtons(
      session = session, inputId = "somevalue",
      choices = newchoices
    )
    updatePickerInput(
      session = session, inputId = "updateselected",
      choices = newchoices
    )
  })
  observeEvent(input$updateselected, {
    updateRadioGroupButtons(
      session = session, inputId = "somevalue",
      selected = input$updateselected
    )
  }, ignoreNULL = TRUE, ignoreInit = TRUE)
  observeEvent(input$updatelabel, {
    updateRadioGroupButtons(
      session = session, inputId = "somevalue",
      label = input$updatelabel
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### updateSliderTextInput

{{< highlight r >}}
updateSliderTextInput(session, inputId, label = NULL, selected = NULL, choices = NULL, from_fixed = NULL, to_fixed = NULL)
{{< /highlight >}}

#### updateSliderTextInputの説明

クライアント上で`sliderTextInput`の値を変更します。

#### updateSliderTextInputの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`label`**|設定するラベル|
|**`selected`**|選択されている値|
|**`choices`**|入力の新しい選択肢|
|**`from_fixed`**|左側のハンドル(または一つのハンドル)を固定|
|**`to_fixed`**|右側のハンドルを固定|

#### updateSliderTextInputの使用例

{{< highlight r >}}
ui <- fluidPage(
  br(),
  sliderTextInput(
    inputId = "mySlider",
    label = "Pick a month :",
    choices = month.abb,
    selected = "Jan"
  ),
  verbatimTextOutput(outputId = "res"),
  radioButtons(
    inputId = "up",
    label = "Update choices:",
    choices = c("Abbreviations", "Full names")
  )
)
server <- function(input, output, session) {
  output$res <- renderPrint(str(input$mySlider))
  observeEvent(input$up, {
    choices <- switch(
      input$up,
      "Abbreviations" = month.abb,
      "Full names" = month.name
    )
    updateSliderTextInput(
      session = session,
      inputId = "mySlider",
      choices = choices
    )
  }, ignoreInit = TRUE)
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}



### updateSpectrumInput

{{< highlight r >}}
updateSpectrumInput(session, inputId, selected)
{{< /highlight >}}

#### updateSpectrumInputの説明

クライアント上で`spectrumInput`の値を変更します。

#### updateSpectrumInputの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`selected`**|選択する値|

#### updateSpectrumInputの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Spectrum color picker"),
  br(),
  spectrumInput(
    inputId = "myColor",
    label = "Pick a color:",
    choices = list(
      list('black', 'white', 'blanchedalmond', 'steelblue', 'forestgreen')
    )
  ),
  verbatimTextOutput(outputId = "res"),
  radioButtons(
    inputId = "update", label = "Update:",
    choices = c(
      'black', 'white', 'blanchedalmond', 'steelblue', 'forestgreen'
    )
  )
)
server <- function(input, output, session) {
  output$res <- renderPrint(input$myColor)
  observeEvent(input$update, {
    updateSpectrumInput(session = session, inputId = "myColor", selected = input$update)
  }, ignoreInit = TRUE)
}
shinyApp(ui, server)
{{< /highlight >}}



### updateSwitchInput

{{< highlight r >}}
updateSwitchInput(session, inputId, value = NULL, label = NULL, onLabel = NULL, offLabel = NULL, onStatus = NULL, offStatus = NULL, disabled = NULL)
{{< /highlight >}}

#### updateSwitchInputの説明

クライアント上で`switchInput`の値を変更します。

#### updateSwitchInputの引数

|名前|説明|
|:--|:--|
|**`session`**|`shinyServer`に与えられた関数に渡されるセッションオブジェクト|
|**`inputId`**|入力オブジェクトのid|
|**`value`**|入力オブジェクトに設定する値|
|**`label`**|入力オブジェクトに設定するラベル|
|**`onLabel`**|入力オブジェクトに設定するオンのときのラベル|
|**`offLabel`**|入力オブジェクトに設定するオフのときのラベル|
|**`onStatus`**|入力オブジェクトに設定するオンのときのステータス|
|**`offStatus`**|入力オブジェクトに設定するオフのときのステータス|
|**`disabled`**|オフの状態を論理値で指定|

#### updateSwitchInputの使用例

{{< highlight r >}}
ui <- fluidPage(
  tags$h1("Update", tags$code("switchInput")),
  br(),
  fluidRow(
    column(
      width = 4,
      panel(
        switchInput(inputId = "switch1"),
        verbatimTextOutput(outputId = "resup1"),
        tags$div(
          class = "btn-group",
          actionButton(
            inputId = "updatevaluetrue",
            label = "Set to TRUE"
          ),
          actionButton(
            inputId = "updatevaluefalse",
            label = "Set to FALSE"
          )
        ),
        heading = "Update value"
      )
    ),
    column(
      width = 4,
      panel(
        switchInput(inputId = "switch2",
                    label = "My label"),
        verbatimTextOutput(outputId = "resup2"),
        textInput(inputId = "updatelabeltext",
                  label = "Update label:"),
        heading = "Update label"
      )
    ),
    column(
      width = 4,
      panel(
        switchInput(
          inputId = "switch3",
          onLabel = "Yeaah",
          offLabel = "Noooo"
        ),
        verbatimTextOutput(outputId = "resup3"),
        fluidRow(column(
          width = 6,
          textInput(inputId = "updateonLabel",
                    label = "Update onLabel:")
        ),
        column(
          width = 6,
          textInput(inputId = "updateoffLabel",
                    label = "Update offLabel:")
        )),
        heading = "Update onLabel & offLabel"
      )
    )
  ),
  fluidRow(column(
    width = 4,
    panel(
      switchInput(inputId = "switch4"),
      verbatimTextOutput(outputId = "resup4"),
      fluidRow(
        column(
          width = 6,
          pickerInput(
            inputId = "updateonStatus",
            label = "Update onStatus:",
            choices = c("default", "primary", "success",
                        "info", "warning", "danger")
          )
        ),
        column(
          width = 6,
          pickerInput(
            inputId = "updateoffStatus",
            label = "Update offStatus:",
            choices = c("default", "primary", "success",
                        "info", "warning", "danger")
          )
        )
      ),
      heading = "Update onStatus & offStatusr"
    )
  ),
  column(
    width = 4,
    panel(
      switchInput(inputId = "switch5"),
      verbatimTextOutput(outputId = "resup5"),
      checkboxInput(
        inputId = "disabled",
        label = "Disabled",
        value = FALSE
      ),
      heading = "Disabled"
    )
  ))
)
server <- function(input, output, session) {
  # Update value
  observeEvent(input$updatevaluetrue, {
    updateSwitchInput(session = session,
                      inputId = "switch1",
                      value = TRUE)
  })
  observeEvent(input$updatevaluefalse, {
    updateSwitchInput(session = session,
                      inputId = "switch1",
                      value = FALSE)
  })
  output$resup1 <- renderPrint({
    input$switch1
  })
  # Update label
  observeEvent(input$updatelabeltext, {
    updateSwitchInput(
      session = session,
      inputId = "switch2",
      label = input$updatelabeltext
    )
  }, ignoreInit = TRUE)
  output$resup2 <- renderPrint({
    input$switch2
  })
  # Update onLabel & offLabel
  observeEvent(input$updateonLabel, {
    updateSwitchInput(
      session = session,
      inputId = "switch3",
      onLabel = input$updateonLabel
    )
  }, ignoreInit = TRUE)
  observeEvent(input$updateoffLabel, {
    updateSwitchInput(
      session = session,
      inputId = "switch3",
      offLabel = input$updateoffLabel
    )
  }, ignoreInit = TRUE)
  output$resup3 <- renderPrint({
    input$switch3
  })
  # Update onStatus & offStatus
  observeEvent(input$updateonStatus, {
    updateSwitchInput(
      session = session,
      inputId = "switch4",
      onStatus = input$updateonStatus
    )
  }, ignoreInit = TRUE)
  observeEvent(input$updateoffStatus, {
    updateSwitchInput(
      session = session,
      inputId = "switch4",
      offStatus = input$updateoffStatus
    )
  }, ignoreInit = TRUE)
  output$resup4 <- renderPrint({
    input$switch4
  })
  # Disabled
  observeEvent(input$disabled, {
    updateSwitchInput(
      session = session,
      inputId = "switch5",
      disabled = input$disabled
    )
  }, ignoreInit = TRUE)
  output$resup5 <- renderPrint({
    input$switch5
  })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}


### useSweetAlert

{{< highlight r >}}
useSweetAlert()
{{< /highlight >}}

#### useSweetAlertの説明

sweet aleartの依存性をロードします。この関数は`sendSweetAlert`, `confirmSweetAlert`, `inputSweetAlert`では不要ですが、`progressSweetAleart`ではまだ必要とされています。

#### useSweetAlertの注記

UI側で`receiveSweetAleart()`を、サーバ側で`sendSweetAlert()`を使用します。