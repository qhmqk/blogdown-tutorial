---
title: "renderImage"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["Rendering functions"]
slug: "renderimage"
weight: 3
description: "画像をレンダリング"
---

{{< highlight r >}}
renderImage(expr, env = parent.frame(), quoted = FALSE, deleteFile = TRUE, outputArgs = list())
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|**`expr`**|リストを返す式|
|**`env`**|中で`expr`を評価するための環境|
|**`quoted`**|`expr`に引用符が付いている(`quoted()`がある)かどうかを指定します。変数内の式を保存したいときに有用です。|
|**`deleteFile`**|クライアントのブラウザに送られた`func()$src`中のファイルを削除するかどうかを指定します。一般的に、画像が$func$内で生成された一時ファイルの場合は`TRUE`、一時ファイルでないなら`FALSE`とします。|
|**`outputArgs`**|`renderImage`を、インタラクティブなR Markdownドキュメントで使用する時に、明示しない`imageOutput`の呼び出しに渡される引数のリストです。|

### 説明

`output`スロットに割り当てる適切な画像を描画します。

### 詳細

式`expr`は、webページ上の`img`オブジェクト属性を持つリストを必ず返します。画像を正しく表示するために、リスト`src`に画像ファイルへのパスとなるエントリが少なくとも1つは必要となります。`contextType`で、画像のMIME型を指定するエントリを持つのが有用です。指定がない場合には、`renderImage`でファイルの拡張子に基づいて型を自動的に検出します。

`width`や`height`, `class`, `alt`などの他の要素も、リストに加えられます。追加の要素は、`img`オブジェクトの属性として使用されます。

対応するHTML出力のタグは、`div`または`img`で、CSSのクラス名は`shiny-image-output`となります。

### 使用例

{{< highlight r >}}
## Only run examples in interactive R sessions
if (interactive()) {
options(device.ask.default = FALSE)

ui <- fluidPage(
  sliderInput("n", "Number of observations", 2, 1000, 500),
  plotOutput("plot1"),
  plotOutput("plot2"),
  plotOutput("plot3")
)

server <- function(input, output, session) {

  # A plot of fixed size
  output$plot1 <- renderImage({
    # A temp file to save the output. It will be deleted after renderImage
    # sends it, because deleteFile=TRUE.
    outfile <- tempfile(fileext='.png')

    # Generate a png
    png(outfile, width=400, height=400)
    hist(rnorm(input$n))
    dev.off()

    # Return a list
    list(src = outfile,
         alt = "This is alternate text")
  }, deleteFile = TRUE)

  # A dynamically-sized plot
  output$plot2 <- renderImage({
    # Read plot2's width and height. These are reactive values, so this
    # expression will re-run whenever these values change.
    width  <- session$clientData$output_plot2_width
    height <- session$clientData$output_plot2_height

    # A temp file to save the output.
    outfile <- tempfile(fileext='.png')

    png(outfile, width=width, height=height)
    hist(rnorm(input$n))
    dev.off()

    # Return a list containing the filename
    list(src = outfile,
         width = width,
         height = height,
         alt = "This is alternate text")
  }, deleteFile = TRUE)

  # Send a pre-rendered image, and don't delete the image after sending it
  # NOTE: For this example to work, it would require files in a subdirectory
  # named images/
  output$plot3 <- renderImage({
    # When input$n is 1, filename is ./images/image1.jpeg
    filename <- normalizePath(file.path('./images',
                              paste('image', input$n, '.jpeg', sep='')))

    # Return a list containing the filename
    list(src = filename)
  }, deleteFile = FALSE)
}

shinyApp(ui, server)
}
{{< /highlight >}}
