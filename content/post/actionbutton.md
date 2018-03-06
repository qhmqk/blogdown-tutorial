---
title: "actionButton"
author: "qhmqk"
date: 2018-02-08
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "actionbutton"
weight: 3
description: "押すことで何らかのアクションを起こすボタンです。`inputId`で指定した値は、ボタンが押される前はNULLで、押された後に0になります。押されるたびに、値が1ずつ増加します。ボタンの押下に対応するコードは、serverで`observeEvent`や`eventReactive`内に記述します。"
---

{{< highlight r >}}
actionButton(inputId, label, icon = NULL, width = NULL, ...)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`inputId`**|値にアクセスするために使用する`input`のスロット|
|**`label`**|ボタンのコンテンツ。文字列を指定するとテキストラベルになり、HTMLを使って画像を指定することもできます。|
|**`icon`**|(オプションで)ボタン上に現れるアイコン|
|**`width`**|'400px'や'100%'などの形式で幅を指定。詳細は`validateCssUnit`を参照|
|**`...`**|ボタンに適用する名前付きの属性|

### 説明

初期値がゼロのアクションボタンを生成し、押されるたびに値を1ずつ増やします。

### 使用例

#### ボタンにアイコンや画像を設定

`icon`を指定することで、ボタンのアイコンを設定できます。画像を設定する場合は、`tags$img`で画像のURLを指定します。`actionButton`と、`tags$button`で`class=btn action-button`とした場合のHTMLは同じになることを利用します。

**このコードでは説明用に、画像への直リンクでボタン上に表示しています。ローカルで実行する限りは問題ありません。しかし、ロゴの著作権はRStudioにあり、直リンクで張り付けたアプリケーションを公開することはできないということに注意してください。**

{{< figure src="/ui-input/actionbuttons-with-icon-and-img.png" alt="Action buttons with icon and img" >}}

{{< highlight r >}}
library(shiny)

ui <- fluidPage(
  fluidRow(
    actionButton("button1", "", icon = icon("th")),
    tags$button(
      id = "button2",
      class="btn action-button",
      icon("close")
    ),
    tags$button(
      id = "button3",
      class = "btn action-button",
      tags$img(src = "https://www.rstudio.com/wp-content/uploads/2014/04/shiny-400x464.png",
               height = "50px")
    )
  ),
  fluidRow(
    textOutput("text")
  )
)

server <- function(input, output, session) {
  out <- reactiveVal("Nothing")
  observeEvent(input$button1,{
    out("left")
  })
  observeEvent(input$button2,{
    out("center")
  })
  observeEvent(input$button3,{
    out("right")
  })
  output$text <- renderText({out()})
}

shinyApp(ui, server)
{{< /highlight >}}

#### アクションボタンの値を使った表示の切り替え

アクションボタンが押されるたびに変化する`input$goButton`の値を用いて、確率密度関数`dnorm`の表示を切り替えます。`%%2`はmod演算子を使って2で割った余りの計算を意味しており、押されるたびに0または1の値との判定をif文で行っています。

{{< figure src="/ui-input/actionbutton-changes-a-histogram.gif" alt="Switching of display using the value of the actionbutton" >}}

{{< highlight r >}}
library(shiny)

ui <- fluidPage(
  actionButton("goButton", "Go!"),
  plotOutput("distPlot")
)

server <- function(input, output) {
  output$distPlot <- renderPlot({
    hist(rnorm(1000), freq = F, xlim = c(-5, 5))
    if (input$goButton%%2 == 0) {
      curve(dnorm, -5, 5, add = T)
    }
  })
}

shinyApp(ui, server)
{{< /highlight >}}

#### 埋め込みCSSを使ったボタンの色の変更

`tags$head`を使って、直接`#button1`の背景色をCSSで指定することで、ボタンの色を変更できます。

{{< highlight r >}}
library(shiny)

ui <- shinyUI(fluidPage(
  tags$head(
    tags$style(HTML('#button1{background-color:red}'))
  ),
  actionButton("button1","red"),
  tags$head(
    tags$style(HTML('#button2{background-color:green}'))
  ),
  actionButton("button2","green"),
  tags$head(
    tags$style(HTML('#button3{background-color:blue}'))
  ),
  actionButton("button3","blue")
))
server <- shinyServer(function(input, output) {
  
})
shinyApp(ui, server)
{{< /highlight >}}

#### shinyjsによるボタンのオンオフ切り替え

shinyjsパッケージを使って、UIに`useShinyjs()`を追加すると、`enable`や`disable`、`toggleState`によりボタンのオンオフを切り替えられるようになります。Entry queryが空の場合は、ボタンをオフに、何らかの文字が入力されている場合はボタンがオンになります。

{{< highlight r >}}
library(shiny)
library(shinyjs)

ui <- fluidPage(
  sidebarLayout(
    sidebarPanel(
      useShinyjs(),
      textInput(inputId = "query", label = "Enter query:", value = ""),
      actionButton(inputId = "search", label = "Search", icon = icon("search"))
    ),
    mainPanel()
  )
)

server <- function(input, output) {
  observe({
    if(is.null(input$query) || input$query == ""){
      disable("search")
    }
    else{
      enable("search")
    }
  })
}

shinyApp(ui = ui, server = server)
{{< /highlight >}}

`toggleState`を用いる場合、サーバの記述を`observe`または`observeEvent`を使って、引数に条件を加えます。

{{< highlight r >}}
observe({
  toggleState("search", input$query != "" | is.null(input$query))
})
{{< /highlight >}}

{{< highlight r >}}
observeEvent(input$query,{
  toggleState("search", input$query != "" | is.null(input$query))
})
{{< /highlight >}}

#### `onclick`を指定してボタンにリンクを追加

引数に`onclick = "window.open('http://google.com', '_blank')"`を指定しています。`onclick`はJavaScriptに依存しているので、環境によっては動作しないことに注意が必要です。

{{< highlight r >}}
library(shiny)

ui <- fluidPage(
  actionButton(inputId='button1', label="open a link", onclick = "window.open('http://google.com', '_blank')")
)

server <- function(input, output) {

}

shinyApp(ui = ui, server = server)
{{< /highlight >}}

### 参照

* RStudioのReference

http://shiny.rstudio.com/articles/action-buttons.html

https://shiny.rstudio.com/reference/shiny/latest/actionButton.html

* stackoverflow

https://stackoverflow.com/questions/44841346/adding-an-image-to-shiny-action-button?rq=1

https://stackoverflow.com/questions/36511847/r-shiny-action-button-to-affect-reactive-control

https://stackoverflow.com/questions/33620133/change-the-color-of-action-button-in-shiny/35871042

https://stackoverflow.com/questions/46891095/disable-action-button-when-textinput-is-empty-in-shiny-app-r?rq=1

https://stackoverflow.com/questions/37795760/r-shiny-add-weblink-to-actionbutton/37796079