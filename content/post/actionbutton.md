---
title: "actionButton"
author: "qhmqk"
date: 2018-01-10
categories: ["Shiny"]
tags: ["UI Inputs"]
slug: "actionbutton"
weight: 3
description: "初期値がゼロのアクションボタンを生成"
---

```{r eval = FALSE}
actionButton(inputId, label, icon = NULL, width = NULL, ...)
```

### 引数

|名前|説明|
|:--|:--|
|`inputId`|値にアクセスするために使用する`input`のスロット|
|`label`|ボタンのコンテンツ。文字列を指定するとテキストラベルになり、HTMLを使って画像を指定することもできます。|
|`icon`|(オプションで)ボタン上に現れるアイコン|
|`width`|'400px'や'100%'などの形式で幅を指定。詳細はvalidateCssUnitを参照|
|`...`|ボタンに適用する名前付きの属性|

### 説明

初期値がゼロのアクションボタンを生成し、押されるたびに値を1ずつ増やします。

### 使用例

* labelに画像を指定



* iconを使用





* inputIdに応じてlabelを変更






### 参照

RStudioのReference

http://shiny.rstudio.com/articles/action-buttons.html

https://shiny.rstudio.com/reference/shiny/latest/actionButton.html

