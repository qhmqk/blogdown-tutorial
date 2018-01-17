---
title: "Shiny app 開発をスタート"
author: "qhmqk"
date: 2018-01-10
categories: ["R"]
tags: ["Shiny"]
weight: 1
slug: "top-page"
description: "最短経路で Shiny の概要を理解してデプロイ"
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
    numericInput(inputId = "n",
        "Sample size", value = 25),
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
||[`actionButton(inputId, label, icon, ...)`]({{< ref "actionbutton.md" >}})|
||[`actionLink(inputId, label, icon, ...)`]()|
||[`checkboxInput(inputId, label, value)`]({{< ref "checkboxinput.md" >}})|
||[`checkboxGroupInput(inputId, label, choices, selected, inline)`]({{< ref "checkboxgroupinput.md" >}})|
||[`dateInput(inputId, label, value, min, max, format, startview, weekstart, language)`]({{< ref "dateinput.md" >}})|
||[`dateRangeInput(inputId, label, start, end, min, max, format, startview, weekstart, language, separator)`]({{< ref "daterangeinput.md" >}})|
||[`fileInput(inputId, label, multiple, accept)`]({{< ref "fileinput.md" >}})|
||[`numericInput(inputId, label, )`]({{< ref "numericinput.md" >}})|
||[`passwordInput(inputId, label, value)`]({{< ref "passwordinput.md" >}})|
||[`radioButtons(inputId, label, choices, selected, inline)`]({{< ref "radiobuttons.md" >}})|
||[`selectInput(inputId, label, choices, selected, multiple, selectize, width, size)`]({{< ref "selectinput.md" >}})|
||[`sliderInput(inputId, label, min, max, value, step, round, format, locate, ticks, animate, width, sep, pre, post)`]({{< ref "sliderinput.md" >}})|
||[`submitButton(text, icon)`]()|
||[`textInput(inputId, label, value)`]({{< ref "textinput.md" >}})|

{{< highlight r >}}
library(shiny)
ui <- fixedPage(
  p(actionButton("actionButton", "Action!")),
  p(actionLink("actionLink", "Link")),
  p(checkboxInput("checkboxInput", "Check")),
  p(checkboxGroupInput("checkboxGroupInput", "Choice:",
                              c("choice 1" = "c1",
                                "choice 2" = "c2",
                                "choice 3" = "c3"))),
  p(dateInput("dateInput", "Date:", value = "2012-02-29")),
  p(dateRangeInput("dateRangeInput", "Date range:",
                 start = "2001-01-01",
                 end   = "2010-12-31")),
  p(fileInput("fileInput", "Choose file:",
            accept = c(
              "text/csv",
              "text/comma-separated-values,text/plain",
              ".csv"))),
  p(numericInput("numericInput", "Numeric", 10, min = 1, max = 100)),
  p(passwordInput("passwordInput", "Password:")),
  p(radioButtons("radioButtons", "Choice:",
                 c("choice 1" = "c1",
                   "choice 2" = "c2",
                   "choice 3" = "c3"))),
  p(selectInput("selectInput", "Choice:",
                 c("choice 1" = "c1",
                   "choice 2" = "c2",
                   "choice 3" = "c3"))),
  p(sliderInput("sliderInput", "Slide:", min = 0, max = 1000, value = 500)),
  p(submitButton(text = "Submit", icon = NULL, width = NULL)),
  p(textInput("textInput", "Text:", "input text"))
)
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

サーバでレンダリングしたオブジェクトを、出力ウィジェットとしてUIに配置して表示します。レンダリング関数をserverに、出力ウィジェット

|レンダリング関数|出力ウィジェット|
|:--|:--|
|`renderPlot(expr, width, height, res, ...)`|`plotOutput(outputId, width, height, )`|
|`renderPrint`|`verbatimTextOutput`|
|`renderText`|`textOutput`|
|`renderUI`|`uiOutput`, `htmlOutput`|
|`renderImage`|`imageOutput`|
|`renderTable`|`tableOutput`|
|`DT::renderDataTable`|`dataTableOutput`|
|||

### レイアウト



### まとめ



### 最後に

Shinyの始め方と、そのシンプルな設計について紹介しました。Rのコーディングだけで、ブラウザ上で動く動的なwebアプリケーションが作れるということで、データを分析するRユーザがShinyを覚えることになるケースが大半だと思います。しかし、それだけでは母集団がRに習熟した人たちだけになってしまい、すそ野が広がっていきません。

HTMLやCSS、JavaScriptを使える人たちが、さらに一歩進んだ分析をwebアプリケーション上に実装したいと思ったときの選択肢として、Shinyが入ってくることを願っています。