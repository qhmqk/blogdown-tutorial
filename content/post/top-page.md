---
title: "Shiny app 開発をスタート"
author: "qhmqk"
date: 2018-01-10
categories: ["R"]
tags: ["Shiny"]
weight: 1
slug: "top-page"
description: "最短経路で Shiny の概要を理解してデプロイ"
toc: true
---

### Shiny って何？(読み飛ばしてオーケー)

R は世界中で広く使用されているプログラミング言語です。Shiny は R のパッケージの一つで、R による分析結果を動的な web アプリケーションとして公開することができます。

R も Shiny もフリーかつオープンソースのソフトウェアとして、開発が進められています。 Rは、多くのプログラミング言語と同様に、Windows、Mac OS、Linuxなどさまざまなプラットフォーム上で動作します。そのため、Shiny による web アプリケーション開発もプラットフォームは問いません。

Shiny を開発しているのは [RStudio Inc.](https://www.rstudio.com/) で、メインの開発者は RStudio の CTO である[Joe Cheng氏](https://github.com/jcheng5)です。

R での分析結果を動的に web アプリケーションにしたい、web アプリケーションに統計や機械学習を組み合わせたい、そんなニーズにこたえる最高の環境が Shiny です。Shiny のインストールから、アプリケーションの作成までを紹介します。

### Shiny を始める前のインストール作業

Shiny で web アプリケーション開発を始める人の大半はすでに R のユーザかもしれませんが、Shiny が気になって開発環境を整えたい人もいるかもしれません。R はダウンロードしてインストールすればすぐにプログラミングを始めることができます。さらに、統合開発環境として、これ以上ないくらい便利なRStudioをインストールすれば、エディタから Shiny の動作確認までボタン一つでできるようになります。インストール作業は、3つだけで初期設定の煩雑さはありません。

1. R をインストール

2. RStudio をインストール

3. Shiny パッケージをインストール

#### R をインストール

[CRAN(The Comprehensive R Archive Network)](https://cran.r-project.org/)からインストーラをダウンロードします。Linux、Mac、Windowsなどのプラットフォームに合わせてバイナリを選択します。

ダウンロードしたR-***.exeを実行し、ウィザードを進めていけば、インストールが完了します。

#### RStudio をインストール

[RStudioの公式サイト](https://www.rstudio.com/products/rstudio/download/)からインストーラをダウンロードします。フリーのRStudio Desctop Open Source Licenseを選択し、Windwos、Mac、Linux (Ubuntu, Fedora)などのプラットフォームに合わせたバイナリを選択します。

#### Shiny パッケージをインストール

RStudioを起動し、パッケージをインストールします。console枠で、

{{< highlight r >}}
install.packages("shiny")
{{< /highlight >}}

を実行すると、Shiny パッケージのインストールが始まります。パッケージをインストール後、Shiny を実行するために以下のコマンドでパッケージをロードします。

{{< highlight r >}}
library(shiny)
{{< /highlight >}}

### Shiny の基本構造とビルド

Shiny を構成する要素は大きく２つだけ、ユーザーインターフェース(ui)とサーバ(server)です。ユーザーインターフェースにはレイアウトやコントロールの配置を記述し、サーバにはユーザーインターフェースに表示する数値やグラフを計算する処理を記述します。

ディレクトリを作り、ディレクトリの中に app.R というファイルを置いて、`runApp()`を実行するだけでShinyアプリケーションが実行されます。最もシンプルなapp.R は以下のコードとなります。

{{< highlight r >}}
library(shiny)
ui <- fluidPage()
server <- function(input, output){}
shinyApp(ui = ui, server = server)
{{< /highlight >}}

このままでは、空のアプリケーションなので、数値入力とヒストグラム表示を追加すると、以下のコードとなります。

{{< highlight r >}}
library(shiny)
ui <- fluidPage(
    numericInput(inputId = "n", "Sample size", value = 25),
    plotOutput(outputId = "hist")
)
server <- function(input, output){
    output$hist <- renderPlot({
        hist(rnorm(input$n))
    })
}
shinyApp(ui = ui, server = server)
{{< /highlight >}}

一つのファイルにまとめて記述するだけでなく、ui.Rとserver.Rという2つのファイルの分けて記述することもできます。その場合も、同様に`runApp()`でShinyアプリケーションが実行されます。((最初は、ui.Rとserver.Rの２つのファイルを別々に記述するよう設計されていましたが、version 0.10.2からapp.Rにまとめて記述して実行できるようになりました。説明の順序とは逆です。))

2つのファイルに分割した場合は、`shinyApp()`が不要です。

ここから、必要に応じてコードを追加していきます。

* ユーザーインターフェースにHTMLのタグやJavaScriptを追加

* サーバに統計解析処理と、グラフ描画を追加

などの処理を記述することができます。

### 入力ウィジェットを配置

ui.R または app.R で `shinyApp` に与える `ui` に、入力コントロールに示す関数を記述します。ユーザからの入力には、`input$<inputId>`でアクセスします。

|入力ウィジェット(図)|関数|
|:--|:--|
|{{< figure src="/ui-input/actionbutton.png" alt="actionButton" >}}|[`actionButton(inputId, label, icon, ...)`]({{< ref "actionbutton.md" >}})|
|{{< figure src="/ui-input/actionlink.png" alt="actionLink" >}}|[`actionLink(inputId, label, icon, ...)`]()|
|{{< figure src="/ui-input/checkboxinput.png" alt="checkboxInput" >}}|[`checkboxInput(inputId, label, value)`]({{< ref "checkboxinput.md" >}})|
|{{< figure src="/ui-input/checkboxgroupinput.png" alt="checkboxGroupInput" >}}|[`checkboxGroupInput(inputId, label, choices, selected, inline)`]({{< ref "checkboxgroupinput.md" >}})|
|{{< figure src="/ui-input/dateinput.png" alt="dateInput" >}}|[`dateInput(inputId, label, value, min, max, format, startview, weekstart, language)`]({{< ref "dateinput.md" >}})|
|{{< figure src="/ui-input/daterangeinput.png" alt="dateRangeInput" >}}|[`dateRangeInput(inputId, label, start, end, min, max, format, startview, weekstart, language, separator)`]({{< ref "daterangeinput.md" >}})|
|{{< figure src="/ui-input/fileinput.png" alt="fileInput" >}}|[`fileInput(inputId, label, multiple, accept)`]({{< ref "fileinput.md" >}})|
|{{< figure src="/ui-input/numericinput.png" alt="numericInput" >}}|[`numericInput(inputId, label, )`]({{< ref "numericinput.md" >}})|
|{{< figure src="/ui-input/passwordinput.png" alt="passwordInput" >}}|[`passwordInput(inputId, label, value)`]({{< ref "passwordinput.md" >}})|
|{{< figure src="/ui-input/radiobuttons.png" alt="radioButtons" >}}|[`radioButtons(inputId, label, choices, selected, inline)`]({{< ref "radiobuttons.md" >}})|
|{{< figure src="/ui-input/selectinput.png" alt="selectInput" >}}|[`selectInput(inputId, label, choices, selected, multiple, selectize, width, size)`]({{< ref "selectinput.md" >}})|
|{{< figure src="/ui-input/sliderinput.png" alt="sliderInput" >}}|[`sliderInput(inputId, label, min, max, value, step, round, format, locate, ticks, animate, width, sep, pre, post)`]({{< ref "sliderinput.md" >}})|
|{{< figure src="/ui-input/submitbutton.png" alt="submitButton" >}}|[`submitButton(text, icon)`]()|
|{{< figure src="/ui-input/textinput.png" alt="textInput" >}}|[`textInput(inputId, label, value)`]({{< ref "textinput.md" >}})|

{{< figure src="/ui-input/input-widgets.png" alt="Major input widgets in vertical layout" >}}

{{< highlight r >}}
library(shiny)

ui <- fluidPage(verticalLayout(
  actionButton("actionButton", "Action!"),
  actionLink("actionLink", "Link"),
  checkboxInput("checkboxInput", "Check"),
  checkboxGroupInput("checkboxGroupInput", "Choice:",
                       c("choice 1" = "c1",
                         "choice 2" = "c2",
                         "choice 3" = "c3")),
  dateInput("dateInput", "Date:", value = "2012-02-29"),
  dateRangeInput("dateRangeInput", "Date range:",
                   start = "2001-01-01",
                   end   = "2010-12-31"),
  fileInput("fileInput", "Choose file:",
              accept = c(
                "text/csv",
                "text/comma-separated-values,text/plain",
                ".csv")),
  numericInput("numericInput", "Numeric", 10, min = 1, max = 100),
  passwordInput("passwordInput", "Password:"),
  radioButtons("radioButtons", "Choice:",
                 c("choice 1" = "c1",
                   "choice 2" = "c2",
                   "choice 3" = "c3")),
  selectInput("selectInput", "Choice:",
                c("choice 1" = "c1",
                  "choice 2" = "c2",
                  "choice 3" = "c3")),
  sliderInput("sliderInput", "Slide:", min = 0, max = 1000, value = 500),
  submitButton(text = "Submit", icon = NULL, width = NULL),
  textInput("textInput", "Text:", "input text")
  ))

server <- function(input, output){
}

shinyApp(ui = ui, server = server)
{{< /highlight >}}


#### actionButton

押すことで何らかのアクションを起こすボタンです。`inputId`で指定した値は、ボタンが押される前はNULLで、押された後に0になります。押されるたびに、値が1ずつ増加します。ボタンの押下に対応するコードは、serverで`observeEvent`や`eventReactive`内に記述します。

#### actionLink

機能はactionButtonと同じで、表示がHTML上のリンク形式になっています。ボタンとは、幅などの見た目の指定がない点などが異なっています。

#### checkboxInput

クリックでチェックの有無を切り替えるチェックボックスです。値はTRUEとFALSEの論理値になっています。

#### checkboxGroupInput

チェックボックスのグループです。それぞれのチェックボックスは独立していますが、uiでコードを記述するときに、ベクトル指定によってまとめて定義できます。

#### dateInput

クリックするとカレンダーのウィジェットが開いて、さらにクリックで特定の日付を選択できます。formatで日付の指定ができるようになっています。`yyyy-mm-dd`で2012年2月29日を選ぶと、`2012-02-29`となります。ハイフン区切りで、年(y)・月(m)・日(d)を指定します。以下のような、記述が可能です。

* `yy` 世紀の部分がない年(12)

* `yyyy` 世紀もついた年(2012)

* `mm` 前に0を挿入した2桁の月(02)

* `m` 0の挿入がない月(2)

* `M` 月の名前の略記(Feb.)

* `MM` 月の名前(February)

* `dd` 前に0を挿入した2桁の日

* `d` 0の挿入がない日

* `D` 曜日の名前の略記

* `DD` 曜日の名前

#### dateRangeInput

dateInputが左右に2つ並んでおり、2つの日付から期間を指定します。

#### fileInput

ファイル選択ダイアログボックスを開きます。ファイルを選択すると、serverにはファイルのpathではなくdataframeが渡されます。dataframeは1行になっており、nameにファイル名、datapathにファイルへのpathが格納されます。

#### numericInput

数値を入力するテキストボックスで、右側に現時点の数値の大きくしたり小さくしたりするボタンがついています。

#### passwordInput

入力した文字列が見えなくなるテキストボックスです。

#### radioButtons

クリックして選択した項目を切り替えるラジオボタンです。

#### selectInput

プルダウンリストやプルダウンメニュー、ドロップダウンメニューなどの名前で呼ばれるクリックすることで、下側に選択肢が広がり、その中から1つを選択します。英語では、select list controlです。

#### sliderInput

ドラッグでバーを左右に動かして数値を指定します。

#### submitButton

押すことで、Shinyアプリケーションの状態が更新されるボタンです。actionButtonと見た目は同じですが、submitButtonを配置すると、ボタン押下のタイミングでのみ表示を更新するアプリケーションを作成できます。**actionButtonを使って、submitButtonと全く同じ機能のプログラムを作成することも可能で、より汎用性のあるactionButtonを使うことが推奨されています**。

#### textInput

文字列を入力するテキストボックスです。

### サーバでレンダリングして、出力ウィジェットで表示

サーバでレンダリングしたオブジェクトを、出力ウィジェットとしてUIに配置して表示します。レンダリング関数をserverに、出力ウィジェットをuiで定義します。

|レンダリング関数|出力ウィジェット|
|:--|:--|
|[`renderImage`]({{< ref "renderimage.md" >}})|`imageOutput`|
|[`renderPlot(expr, width, height, res, ...)`]({{< ref "renderplot.md" >}})|`plotOutput(outputId, width, height, )`|
|[`renderPrint`]({{< ref "renderprint.md" >}})|`verbatimTextOutput`|
|[`renderTable`]({{< ref "rendertable.md" >}})|`tableOutput`|
|[`renderText`]({{< ref "rendertext.md" >}})|`textOutput`|
|[`renderUI`]({{< ref "renderui.md" >}})|`uiOutput`, `htmlOutput`|
|`DT::renderDataTable`|`dataTableOutput`|
|||

### リアクティビティ(Reactivity) を定義

入力ウィジェットでユーザが何らかの操作を行い、サーバでレンダリングして出力ウィジェットで表示するまでの処理の部分を、Shiny ではリアクティブプログラミングで実現します。R を用いたデータ解析ではあまり馴染みのない言葉ですが、基本的な考え方は難しくありません。

#### もっとも単純な実装

入力と出力を直接 server で定義した関数で結ぶ構造がもっとも単純です。最初に示した数値入力とヒストグラムは、この構造になっています。

{{< highlight r >}}
numericInput(inputId = "n", "Sample size", value = 25),
plotOutput(outputId = "hist")
{{< /highlight >}}

ユーザが数値を入力するたびに、server では`input$n`の値が更新されます。`output$hist`の値が更新されるたびに、`plotOutput`でプロットを再描画します。

{{< highlight r >}}
output$hist <- renderPlot({
    hist(rnorm(input$n))
})
{{< /highlight >}}

server では`renderPlot`により、`input$n`を引数として直接`output$hist`の値を変化させる構造になっています。入力と出力の間が関数のみなので、この形がもっとも単純な実装です。

#### 単純な実装を拡張して、複数入力、複数出力、reactive 関数による計算過程のカプセル化

入力をサンプルサイズと、幅の2つにします。出力は、先ほどと同様のヒストグラムです。

{{< highlight r >}}
# ui
numericInput(inputId = "n", "Sample size", value = 25),
numericInput(inputId = "b", "Breaks", value = 5),
plotOutput(outputId = "hist")
{{< /highlight >}}

サーバでは、`input$n`と`input$b`の値から、ヒストグラムを作成し、`renderPlot`で出力オブジェクトを生成します。

{{< highlight r >}}
# server
output$hist <- renderPlot({
    hist(rnorm(input$n), breaks = input$b)
})
{{< /highlight >}}

`renderPlot`は、`input$n`または`input$b`のどちらかの値が変わるたびに再度実行されて、表示が更新されます。

次に、一つの入力に対して、複数の出力を実現します。

{{< highlight r >}}
# ui
numericInput(inputId = "n", "Factorial of", value = 1, min = 1, max = 100)
textOutput("factorial_n")
textOutput("factorial_n_inv")
{{< /highlight >}}

`numericInput`で入力した値の階乗、階乗の逆数の2つの値を計算して出力します。

{{< highlight r >}}
# server
output$factorial_n <- renderText({gamma(input$n)})
output$factorial_n_inv <- renderText({ 1 / gamma(input$n)})
{{< /highlight >}}

入力 n の値が更新されるたびに、2つの出力が更新される単純なリアクティビティを定義しました。見ると明らかなように、`renderText`内で`gamma()`を実行しており、入力が変化するたびに`gamma()`を2回実行することになります。入力から計算した値を、複数の出力で使う、あるいは中間変数とする場合に使用するのが`reactive`関数です。

Shiny のリアクティビティを定義するときに必要となるリアクティブプログラミングでは、中間変数そのものをサーバでは定義しません(できません)。そのため、`reactive`で、`gamma()`の計算を、入力変化のたびに毎回再計算される関数として定義します。

{{< highlight r >}}
# server
current_fact <- reactive({gamma(input$n)})

output$factorial_n <- renderText(current_fact())
output$factorial_n_inv = renderText({ 1 / current_fact()})
{{< /highlight >}}

`current_fact`は、入力が変化するたびに実行する計算をカプセル化したものになります。このカプセル化により、`gamma()`の実行は1回で済むようになります。

### レイアウト

Shiny のレイアウトは、3段階に分けて考えます。

1. パネルによる要素の結合

2. ページの設計

3. タブメニューとナビゲーションバー

#### パネルによる要素の結合

入力や出力UIを一つの要素にまとめる場合に、パネル関数を使用します。

{{< highlight r >}}
wellPanel(
    actionButton("actionButton", "Action!"),
    checkboxInput("checkboxInput", "Check")
)
{{< /highlight >}}

#### ページの設計

パネルを含む各要素を、レイアウト関数を用いてページ内に配置します。

* fluidRow()

幅が可変の行を設定します。行中の列要素が`column`です。Bootstrapによるデザインでは、一行の幅を12として、各列の`width`, `offset`を指定します。

{{< highlight r >}}
ui <- fluidPage(
    fluidRow(column(width = 4), cokumin(width = 2, offset = 3)),
    fluidRow(column(width = 12))
)
{{< /highlight >}}

* flowLayout()

要素を順に横に並べます。表示する幅に応じて、改行されて配置されます。

{{< highlight r >}}
ui <- fluidPage(
    flowLayout(
        # object 1,
        # object 2,
        # object 3
    )
)
{{< /highlight >}}

* sidebarLayout()

1つのページをサイドパネル(`sidebarPanel`)とメインパネル(`mainPanel`)に分割するレイアウトです。

{{< highlight r >}}
ui <- fluidPage(
    sidebarLayout(
        sidebarPanel(),
        mainPanel()
    )
)
{{< /highlight >}}

* splitLayout()

一つのページを縦に分割するレイアウトです。

{{< highlight r >}}
ui <- fluidPage(
    splitLayout(
        # object 1,
        # object 2
    )
)
{{< /highlight >}}

* verticalLayout()

要素を縦に配置していくレイアウトです。

{{< highlight r >}}
ui <- fluidPage(
    verticalLayout(
        # object 1,
        # object 2,
        # object 3
    )
)
{{< /highlight >}}

#### タブメニューとナビゲーションバー

* タブ

{{< highlight r >}}
ui <- fluidPage(
    tabsetPanel(
        tabPanel("tab 1", "contents"),
        tabPanel("tab 2", "contents"),
        tabPanel("tab 3", "contents")
    )
)
{{< /highlight >}}

* ナビゲーションリスト

{{< highlight r >}}
ui <- fluidPage(
    nablistPanel(
        tabPanel("tab 1", "contents"),
        tabPanel("tab 2", "contents"),
        tabPanel("tab 3", "contents")
    )
)
{{< /highlight >}}

* ナビゲーションページ

{{< highlight r >}}
ui <- fluidPage(
    navbarPage(
        tabPanel("tab 1", "contents"),
        tabPanel("tab 2", "contents"),
        tabPanel("tab 3", "contents")
    )
)
{{< /highlight >}}

タブやナビゲーションバーを用いてダッシュボードを設計する場合は、`tabsetPanel`や`navbarPage`よりも、`shinydashboard`パッケージを用いるのが便利です。

### Shiny アプリケーションの共有、またはサービスとしての立ち上げ

RStudioから最も簡単に Shiny アプリケーションを共有する場合、shinyapps.ioがおすすめです。shinyapps.ioを利用する手順は、

1. http://shinyapps.ioでアカウントを作成

2. RStudioから`rsconnect::deployApp("path")`を実行(pathにはShinyアプリケーションのディレクトリが入ります)

shinyapps.ioを使わない場合は、AWSなどのサービスを利用して、Shiny Serverを設置することで公開することとなります。

### まとめ

Shiny を始めるために最低限必要となる手順について説明しました。インストール作業を終えると、RStudioだけでShinyの開発に十分な機能が揃っています。

UIに配置する入力と出力ウィジェットを決めて、サーバに計算処理を記述します。入出力の関係は、リアクティブプログラミングと呼ばれる形式でリアクティビティを定義します。

配置した入出力ウィジェットは、レイアウト関数により任意の配置が可能です。Shiny はBootstrapで設計されているので、`fluidPage`のような可変レイアウト用の関数を用いるとブラウザの表示幅ごとにレスポンシブなデザインで表示されます。

Shiny アプリケーションを公開するための第一選択肢が、shinyapps.ioです。2018年2月時点で5個までであれば、無料で公開することができます。AWSなどのクラウドサービスを利用する場合、Shiny Serverを設置することとなります。

### 最後に

Shinyの始め方と、そのシンプルな設計について紹介しました。Rのコーディングだけで、ブラウザ上で動く動的なwebアプリケーションが作れるということで、データを分析するRユーザがShinyを覚えることになるケースが大半だと思います。しかし、それだけでは母集団がRに習熟した人たちだけになってしまい、すそ野が広がっていきません。

HTMLやCSS、JavaScriptを使える人たちが、さらに一歩進んだ分析をwebアプリケーション上に実装したいと思ったときの選択肢として、Shinyが入ってくることを願っています。