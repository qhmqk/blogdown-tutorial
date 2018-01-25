---
title: "renderPlot"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["Rendering functions"]
slug: "renderplot"
weight: 3
description: "プロットをレンダリング"
---

{{< highlight r >}}
renderPlot(expr, width = "auto", height = "auto", res = 72, ..., env = parent.frame(), quoted = FALSE, execOnResize = FALSE, outputArgs = list())
{{< /highlight >}}

### 引数

|名前|説明|
|:--|:--|
|`expr`|プロットを生成する式|
|`width`, `height`|描画するプロットの高さと幅をピクセルで指定します。`auto`を指定して、HTMLの`offsetWidth`と`offsetHeight`を用いることもできます。インラインでプロットするときには、数値で`width`と`height`を必ず指定します。|
|`res`|インチ単位のピクセル解像度を指定します。この値は、`png`に渡されます。Rで描画するPNGの解像度を変えるのであって、ブラウザの実際のppiを変えるわけではないことに注意してください。|
|...|幅、高さや背景色などの`png`に渡す引数|
|`env`|中で`expr`を評価するための環境|
|`quoted`|`expr`に引用符が付いている(`quoted()`がある)かどうかを指定します。変数内の式を保存したいときに有用です。|
|`execOnResize`|(デフォルトの)`FALSE`なら、プロットのサイズ決定が繰り返され、Shinyは`expr`の再実行の代わりに、`replayPlot()`コマンドでプロットの描画を繰り返します。これにより、高速な再描画が可能となります。まれに望ましくない場合もあります。プロットのサイズ決定やり直しに問題がある場合に、`TRUE`を設定してShinyのコードを再実行することができます。|
|`outputArgs`|`renderImage`を、インタラクティブなR Markdownドキュメントで使用する時に、明示しない`imageOutput`の呼び出しに渡される引数のリストです。|

### 説明

出力スロットに割り当てるのに適したリアクティブなプロットを描画します。

### 詳細

出力に対応するHTMLのタグは`div`または`img`で、`shiny-plot-output`という名前のCSSクラスを持ちます。

### インタラクティブなプロット

ggplot2による作図の場合、`renderPlot`はggplotのオブジェクトを返すべきです。一方で、もしコードが`print(p)`のようにggplot2オブジェクトを出力するなら、インタラクティブな作図の座標は、データの空間に適切に縮小・拡大されないでしょう。

インタラクティブなプロットについて、詳細な情報が欲しい場合は、`plotOutput`を確認してください。

### 参照

https://shiny.rstudio.com/reference/shiny/latest/renderPlot.html