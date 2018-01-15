---
title: "トップページ"
author: "qhmqk"
date: 2018-01-10
categories: ["R"]
tags: ["Shiny"]
weight: 1
slug: "top-page"
description: "今すぐ始めるShiny2"
---

今すぐ始めるShiny

Rは世界中で広く使用されているプログラミング言語です。ShinyはRのパッケージの一つで、Rによる分析結果を動的なwebアプリケーションとして公開することができます。


[test link]({{< ref "migrate-from-jekyll.md" >}})

RもShinyもフリーかつオープンソースのソフトウェアとして、開発が進められています。Rは、多くのプログラミング言語と同様に、Windows、Mac OS、Linuxなどさまざまなプラットフォーム上で動作します。そのため、Shinyによるwebアプリケーション開発もプラットフォームは問いません。

Shinyを開発しているのはRStudio Inc.で、メインの開発者はRStudioのCTOである[Joe Cheng氏](https://github.com/jcheng5)です。

Rでの分析結果を動的にwebアプリケーションにしたい、webアプリケーションに統計や機械学習を組み合わせたい、そんなニーズにこたえる最高の環境がShinyです。Shinyのインストールから、アプリケーションの作成までを紹介します。

### すぐに始められるShiny

Shinyでwebアプリケーション開発を始める人の大半はすでにRのユーザかもしれませんが、Shinyが気になって開発環境を整えたい人もいるかもしれません。Rはダウンロードしてインストールすればすぐにプログラミングを始めることができます。さらに、統合開発環境として、これ以上ないくらい便利なRStudioをインストールすれば、エディタからShinyの動作確認までボタン一つでできるようになります。インストール作業は、3つだけで初期設定の煩雑さはありません。

1. Rをインストール

2. RStudioをインストール

3. Shinyパッケージをインストール

#### Rをインストール

[CRAN(The Comprehensive R Archive Network)](https://cran.r-project.org/)からインストーラをダウンロードします。Linux、Mac、Windowsなどのプラットフォームに合わせてバイナリを選択します。

ダウンロードしたR-***.exeを実行し、ウィザードを進めていけば、インストールが完了します。

#### RStudioをインストール

[RStudioの公式サイト](https://www.rstudio.com/products/rstudio/download/)からインストーラをダウンロードします。フリーのRStudio Desctop Open Source Licenseを選択し、Windwos、Mac、Linux (Ubuntu, Fedora)などのプラットフォームに合わせたバイナリを選択します。

#### Shinyパッケージをインストール

RStudioを起動し、パッケージをインストールします。console枠で、

```r
install.packages("shiny")
```

を実行すると、Shinyパッケージのインストールが始まります。パッケージをインストール後、Shinyを実行するために以下のコマンドでパッケージをロードします。

```r
library(shiny)
```

### Shinyのシンプルな設計

Shinyを構成する要素は大きく２つだけ、ユーザーインターフェース(ui)とサーバ(server)です。ユーザーインターフェースにはレイアウトやコントロールの配置を記述し、サーバにはユーザーインターフェースに表示する数値やグラフを計算する処理を記述します。

ディレクトリを作り、ディレクトリの中にapp.Rというファイルを置いて、`runApp()`を実行するだけでShinyアプリケーションが実行されます。最もシンプルなapp.Rは以下のコードとなります。

```r
library(shiny)
ui <- fluidPage()
server <- function(input, output){}
shinyApp(ui = ui, server = server)
```

このままでは、空のアプリケーションなので、数値入力とヒストグラム表示を追加すると、以下のコードとなります。

```r
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
```

一つのファイルにまとめて記述するだけでなく、ui.Rとserver.Rという2つのファイルの分けて記述することもできます。その場合も、同様に`runApp()`でShinyアプリケーションが実行されます。((最初は、ui.Rとserver.Rの２つのファイルを別々に記述するよう設計されていましたが、version 0.10.2からapp.Rにまとめて記述して実行できるようになりました。説明の順序とは逆です。))

2つのファイルに分割した場合は、`shinyApp()`が不要です。

ここから、必要に応じてコードを追加していきます。

* ユーザーインターフェースにHTMLのタグやJavaScriptを追加

* サーバに統計解析処理と、グラフ描画を追加

などの処理を記述することができます。

### 最後に

Shinyの始め方と、そのシンプルな設計について紹介しました。Rのコーディングだけで、ブラウザ上で動く動的なwebアプリケーションが作れるということで、データを分析するRユーザがShinyを覚えることになるケースが大半だと思います。しかし、それだけでは母集団がRに習熟した人たちだけになってしまい、すそ野が広がっていきません。

HTMLやCSS、JavaScriptを使える人たちが、さらに一歩進んだ分析をwebアプリケーション上に実装したいと思ったときの選択肢として、Shinyが入ってくればいいですね。