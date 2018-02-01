---
title: "plotOutput"
author: "qhmqk"
date: 2018-02-01
categories: ["Shiny"]
tags: ["UI Outputs"]
slug: "plotoutput"
weight: 3
description: "プロットを出力"
---

{{< highlight r >}}
plotOutput(outputId, width = "100%", height = "400px", click = NULL, dblclick = NULL, hover = NULL, hoverDelay = NULL, hoverDelayType = NULL, brush = NULL, clickId = NULL, w1hoverId = NULL, inline = FALSE)
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|`outputId`|プロット/画像を読み込む出力変数|
|`width`, `height`|画像の幅と高さ。適切なCSSの単位("100%"や"400px"、"auto")を付けて指定します。数値は強制的に"px"が付けられた値となります。`inline = TRUE`のとき、2つの引数は無視されて、プロットの幅と高さは`renderPlot()`の中で指定されます。HTML/CSSで記述された通りに高さが計算されるため、`height`に"auto"や"100%"を指定すると期待通りに動かないであろうことに注意して下さい。|
|`click`|`NULL`(デフォルト)、文字列、または`clickOpts`関数で生成されるオブジェクトを指定します。"plot_click"(または、等価な`clickOpts(id = "plot_click")`)のような値を用いると、クリックするたびにプロットが座標をサーバに送信します。値は、`input$plot_click`でアクセス可能で、マウスの場所を指す`x`と`y`の名前付きのリストです。|
|`dbclick`|ダブルクリックのイベントに対応する変数で、`click`と同様です。|
|`hover`|`click`と同様に、`NULL`(デフォルト)、文字列、または`hoverOpts`関数で生成されるオブジェクトを指定します。"plot_hover"(または、等価な`hoverOpts(id = "plot_hover")`)のような値を用いると、プロット上でとどまっている座標をサーバに送信します。値は、`input$plot_hover`でアクセス可能で、マウスの場所を指す`x`と`y`の名前付きのリストです。hoverの時間と遅延時間を制御するためには、`hoverOpts`を使う必要があります。|
|`hoverDelay`|非推奨で、代わりに`hover`を使うことが推奨されます。`hoverOpts`関数を参照してください。|
|`hoverDelayType`|非推奨で、代わりに`hover`を使うことが推奨されます。`hoverOpts`関数を参照してください。|
|`brush`|`click`と同様に、`NULL`(デフォルト)、文字列、または`brushOpts`関数で生成されるオブジェクトを指定します。"plot_brush"(または、等価な`brushOpts(id = "plot_brush")`)のような値を用いると、プロット領域内でユーザにブラシさせることができます。ブラシされた領域の情報はサーバに送られ、その値は`input$plot_brush`でアクセス可能です。ブラシはユーザがプロット領域で矩形を描いてそれをドラッグすることを意味します。値はブラシ領域を指す名前付きリストで要素に`xmin`と`xmax`, `ymin`, `ymax`があります。ブラシの動きを制御するために、`brushOpts`を使用します。複数の`imageOutput/plotOutput`呼び出しが、同じ`id`値を共有します。すなわち、ある画像またはプロットをブラシすると、他のブラシも同じ`id`を持つので消えます。|
|`clickId`|非推奨で、代わりに`click`を使うことが推奨されます。`clickOpts`関数を参照してください。|
|`hoverId`|非推奨で、代わりに`hover`を使うことが推奨されます。`hoverOpts`関数を参照してください。|
|`inline`|出力にインライン(`span()`)、またはブロックコンテナ(`div()`)を使用します。|

### 値

パネル内に含まれるプロットまたは画像出力要素

### 説明

アプリケーションのページ内で、`renderPlot`または`renderImage`をレンダリングします。

### 注記

引数の`clickId`と`hoverId`は、Rの基本グラフィックでのみ動作します(graphicsパッケージを見て下さい)ggplot2やlatticeなどのようなグリッドに基づくグラフィックでは動作しません。

### インタラクティブなプロット

Shinyのプロットと画像は、クリックやダブルクリック、ホバー、ブラシなどのマウス操作をサポートします。これらのインタラクティブな操作イベントが起きると、マウス座標が`input$`変数としてサーバに送られ、`click`, `dbclick`, `hover`, `brush`の指定で参照できます。

`plotOutput`では、可能であれば、座標はデータ空間に拡大縮小されてサーバに送られます(基本的なgraphicsとggplot2で生成されたプロットは、この拡大縮小をサポートしています。一方、latticeと他のもので生成されたプロットはサポートしていません)。拡大縮小できない場合、そのままのピクセル座標が送られます。`imageOutput`では、座標は常にそのままのピクセル座標となります。

ggplot2の作図では、`renderPlot`中のコードはggplotオブジェクトを返します。コードが`print(p)`のようにggplot2オブジェクトをプリントするなら、インタラクティブな作図の座標はデータ空間に適切に拡大縮小されません。

### 使用例

{{< highlight r >}}
# Only run these examples in interactive R sessions
if (interactive()) {

# A basic shiny app with a plotOutput
shinyApp(
  ui = fluidPage(
    sidebarLayout(
      sidebarPanel(
        actionButton("newplot", "New plot")
      ),
      mainPanel(
        plotOutput("plot")
      )
    )
  ),
  server = function(input, output) {
    output$plot <- renderPlot({
      input$newplot
      # Add a little noise to the cars data
      cars2 <- cars + rnorm(nrow(cars))
      plot(cars2)
    })
  }
)


# A demonstration of clicking, hovering, and brushing
shinyApp(
  ui = basicPage(
    fluidRow(
      column(width = 4,
        plotOutput("plot", height=300,
          click = "plot_click",  # Equiv, to click=clickOpts(id="plot_click")
          hover = hoverOpts(id = "plot_hover", delayType = "throttle"),
          brush = brushOpts(id = "plot_brush")
        ),
        h4("Clicked points"),
        tableOutput("plot_clickedpoints"),
        h4("Brushed points"),
        tableOutput("plot_brushedpoints")
      ),
      column(width = 4,
        verbatimTextOutput("plot_clickinfo"),
        verbatimTextOutput("plot_hoverinfo")
      ),
      column(width = 4,
        wellPanel(actionButton("newplot", "New plot")),
        verbatimTextOutput("plot_brushinfo")
      )
    )
  ),
  server = function(input, output, session) {
    data <- reactive({
      input$newplot
      # Add a little noise to the cars data so the points move
      cars + rnorm(nrow(cars))
    })
    output$plot <- renderPlot({
      d <- data()
      plot(d$speed, d$dist)
    })
    output$plot_clickinfo <- renderPrint({
      cat("Click:\n")
      str(input$plot_click)
    })
    output$plot_hoverinfo <- renderPrint({
      cat("Hover (throttled):\n")
      str(input$plot_hover)
    })
    output$plot_brushinfo <- renderPrint({
      cat("Brush (debounced):\n")
      str(input$plot_brush)
    })
    output$plot_clickedpoints <- renderTable({
      # For base graphics, we need to specify columns, though for ggplot2,
      # it's usually not necessary.
      res <- nearPoints(data(), input$plot_click, "speed", "dist")
      if (nrow(res) == 0)
        return()
      res
    })
    output$plot_brushedpoints <- renderTable({
      res <- brushedPoints(data(), input$plot_brush, "speed", "dist")
      if (nrow(res) == 0)
        return()
      res
    })
  }
)


# Demo of clicking, hovering, brushing with imageOutput
# Note that coordinates are in pixels
shinyApp(
  ui = basicPage(
    fluidRow(
      column(width = 4,
        imageOutput("image", height=300,
          click = "image_click",
          hover = hoverOpts(
            id = "image_hover",
            delay = 500,
            delayType = "throttle"
          ),
          brush = brushOpts(id = "image_brush")
        )
      ),
      column(width = 4,
        verbatimTextOutput("image_clickinfo"),
        verbatimTextOutput("image_hoverinfo")
      ),
      column(width = 4,
        wellPanel(actionButton("newimage", "New image")),
        verbatimTextOutput("image_brushinfo")
      )
    )
  ),
  server = function(input, output, session) {
    output$image <- renderImage({
      input$newimage

      # Get width and height of image output
      width  <- session$clientData$output_image_width
      height <- session$clientData$output_image_height

      # Write to a temporary PNG file
      outfile <- tempfile(fileext = ".png")

      png(outfile, width=width, height=height)
      plot(rnorm(200), rnorm(200))
      dev.off()

      # Return a list containing information about the image
      list(
        src = outfile,
        contentType = "image/png",
        width = width,
        height = height,
        alt = "This is alternate text"
      )
    })
    output$image_clickinfo <- renderPrint({
      cat("Click:\n")
      str(input$image_click)
    })
    output$image_hoverinfo <- renderPrint({
      cat("Hover (throttled):\n")
      str(input$image_hover)
    })
    output$image_brushinfo <- renderPrint({
      cat("Brush (debounced):\n")
      str(input$image_brush)
    })
  }
)

}
{{< /highlight >}}

### 参照

https://shiny.rstudio.com/reference/shiny/1.0.5/plotOutput.html