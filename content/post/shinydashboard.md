---
title: "shinydashboard"
author: "qhmqk"
date: 2018-02-15
categories: ["Shiny"]
tags: ["Packages"]
slug: "shinydashboard"
weight: 4
description: "ダッシュボードを作成"
toc: true
---

### box

ダッシュボード本体のボックスを生成します。ボックスはダッシュボード本体の中にコンテンツ置くために用います。

{{< highlight r >}}
box(..., title = NULL, footer = NULL, status = NULL,
  solidHeader = FALSE, background = NULL, width = 6, height = NULL,
  collapsible = FALSE, collapsed = FALSE)
{{< /highlight >}}

#### 引数

|名前|説明|
|:--|:--|
|**`...`**|`box`のコンテンツ|
|**`title`**|オプションで指定するタイトル|
|**`footer`**|オプションで指定するフッタのテキスト|
|**`status`**|項目の状態。背景色はここで設定します。有効な状態は、`validStatuses`のリストになります。|
|**`solidHeader`**|ヘッダを無色で表示するかどうかを指定|
|**`background`**|`NULL`(デフォルト)の場合、ボックスの背景は白色となります。それ以外は、色を文字列で指定します。有効な色は、`validColors`のリストになります。|
|**`width`**|Bootstrapのグリッドシステムにおけるボックスの幅。行ベースのレイアウトで用いられます。最大の幅は12で、デフォルトの`valueBox`の幅は4なので1/3の幅を占めます。列ベースのレイアウトでは、幅に`NULL`を用います。すなわち幅はボックスを持つ列によって設定されます。|
|**`height`**|ボックスの高さをピクセルまたは他のCSSの単位で指定します。デフォルトでは、高さはコンテンツに応じて自動的に拡大縮小します。|
|**`collapsible`**|`TRUE`の場合、右上にボックスを掴むためのボタンを表示します。|
|**`collapsed`**|`TRUE`の場合、掴んだ状態で開始されます。`collapsible = TRUE`である必要があります。|

#### 使用例

{{< highlight r >}}
## Only run this example in interactive R sessions
if (interactive()) {
library(shiny)

# A dashboard body with a row of infoBoxes and valueBoxes, and two rows of boxes
body <- dashboardBody(

  # infoBoxes
  fluidRow(
    infoBox(
      "Orders", uiOutput("orderNum2"), "Subtitle", icon = icon("credit-card")
    ),
    infoBox(
      "Approval Rating", "60%", icon = icon("line-chart"), color = "green",
      fill = TRUE
    ),
    infoBox(
      "Progress", uiOutput("progress2"), icon = icon("users"), color = "purple"
    )
  ),

  # valueBoxes
  fluidRow(
    valueBox(
      uiOutput("orderNum"), "New Orders", icon = icon("credit-card"),
      href = "http://google.com"
    ),
    valueBox(
      tagList("60", tags$sup(style="font-size: 20px", "%")),
       "Approval Rating", icon = icon("line-chart"), color = "green"
    ),
    valueBox(
      htmlOutput("progress"), "Progress", icon = icon("users"), color = "purple"
    )
  ),

  # Boxes
  fluidRow(
    box(status = "primary",
      sliderInput("orders", "Orders", min = 1, max = 2000, value = 650),
      selectInput("progress", "Progress",
        choices = c("0%" = 0, "20%" = 20, "40%" = 40, "60%" = 60, "80%" = 80,
                    "100%" = 100)
      )
    ),
    box(title = "Histogram box title",
      status = "warning", solidHeader = TRUE, collapsible = TRUE,
      plotOutput("plot", height = 250)
    )
  ),

  # Boxes with solid color, using `background`
  fluidRow(
    # Box with textOutput
    box(
      title = "Status summary",
      background = "green",
      width = 4,
      textOutput("status")
    ),

    # Box with HTML output, when finer control over appearance is needed
    box(
      title = "Status summary 2",
      width = 4,
      background = "red",
      uiOutput("status2")
    ),

    box(
      width = 4,
      background = "light-blue",
      p("This is content. The background color is set to light-blue")
    )
  )
)

server <- function(input, output) {
  output$orderNum <- renderText({
    prettyNum(input$orders, big.mark=",")
  })

  output$orderNum2 <- renderText({
    prettyNum(input$orders, big.mark=",")
  })

  output$progress <- renderUI({
    tagList(input$progress, tags$sup(style="font-size: 20px", "%"))
  })

  output$progress2 <- renderUI({
    paste0(input$progress, "%")
  })

  output$status <- renderText({
    paste0("There are ", input$orders,
      " orders, and so the current progress is ", input$progress, "%.")
  })

  output$status2 <- renderUI({
    iconName <- switch(input$progress,
      "100" = "ok",
      "0" = "remove",
      "road"
    )
    p("Current status is: ", icon(iconName, lib = "glyphicon"))
  })


  output$plot <- renderPlot({
    hist(rnorm(input$orders))
  })
}

shinyApp(
  ui = dashboardPage(
    dashboardHeader(),
    dashboardSidebar(),
    body
  ),
  server = server
)
}
{{< /highlight >}}

Documentation reproduced from package shinydashboard, version 0.6.1, License: GPL-2 | file LICENSE

### dashboardBody

ダッシュボードページの本体を生成します。本体は通常、コンテンツとしてボックスを持ちます。ボックス以外であれば、`tabItems`を持つ場合があります。

{{< highlight r >}}
dashboardBody(...)
{{< /highlight >}}

#### 引数

|名前|説明|
|:--|:--|
|**`...`**|ダッシュボード本体に置く項目|

#### 使用例

{{< highlight r >}}
library("shinydashboard")

header <- dashboardHeader()

sidebar <- dashboardSidebar()

body <- dashboardBody(
                h2('Something here!!!')
          )

shinyApp(
  ui = dashboardPage(header, sidebar, body),
  server = function(input, output) {}
    )
  }
)
{{< /highlight >}}

### dashboardHeader

ダッシュボードページのヘッダを生成します。ダッシュボードのヘッダは空白、または右側にドロップダウンメニューの項目を持ちます。

{{< highlight r >}}
dashboardHeader(..., title = NULL, titleWidth = NULL, disable = FALSE,
  .list = NULL)
{{< /highlight >}}

#### 引数

|名前|説明|
|:--|:--|
|**`...`**|ヘッダに置く項目。`dropdownMenus`です。|
|**`title`**|ヘッダバーにオプションで表示するタイトル。デフォルトでは、ブラウザのタイトルバーに表示されるタイトルとしても用いられます。ダッシュボードヘッダバーのテキストと違うタイトルにしたい場合は、`dashboardPage`で`title`を設定します。|
|**`titleWidth`**|タイトルを表示する領域の幅。ピクセルまたはCSSの単位を付けた文字列で幅を指定する必要があります。|
|**`disable`**|`TRUE`なら、ヘッダバーを表示しません。|
|**`.list`**|ヘッダに置く項目を含むオプションのリスト。`...`と同じですが、リストのフォーマットです。プログラム上で項目を生成しながら動作させるときに役立ちます。|

#### 使用例

{{< highlight r >}}
## Only run this example in interactive R sessions
if (interactive()) {
library(shiny)

# A dashboard header with 3 dropdown menus
header <- dashboardHeader(
  title = "Dashboard Demo",

  # Dropdown menu for messages
  dropdownMenu(type = "messages", badgeStatus = "success",
    messageItem("Support Team",
      "This is the content of a message.",
      time = "5 mins"
    ),
    messageItem("Support Team",
      "This is the content of another message.",
      time = "2 hours"
    ),
    messageItem("New User",
      "Can I get some help?",
      time = "Today"
    )
  ),

  # Dropdown menu for notifications
  dropdownMenu(type = "notifications", badgeStatus = "warning",
    notificationItem(icon = icon("users"), status = "info",
      "5 new members joined today"
    ),
    notificationItem(icon = icon("warning"), status = "danger",
      "Resource usage near limit."
    ),
    notificationItem(icon = icon("shopping-cart", lib = "glyphicon"),
      status = "success", "25 sales made"
    ),
    notificationItem(icon = icon("user", lib = "glyphicon"),
      status = "danger", "You changed your username"
    )
  ),

  # Dropdown menu for tasks, with progress bar
  dropdownMenu(type = "tasks", badgeStatus = "danger",
    taskItem(value = 20, color = "aqua",
      "Refactor code"
    ),
    taskItem(value = 40, color = "green",
      "Design new layout"
    ),
    taskItem(value = 60, color = "yellow",
      "Another task"
    ),
    taskItem(value = 80, color = "red",
      "Write documentation"
    )
  )
)

shinyApp(
  ui = dashboardPage(
    header,
    dashboardSidebar(),
    dashboardBody()
  ),
  server = function(input, output) { }
)
}
{{< /highlight >}}

shinydashboard, version 0.6.1, License: GPL-2

### dashboardPage

Shiny appにダッシュボードページを生成します。

{{< highlight r >}}
dashboardPage(header, sidebar, body, title = NULL, skin = c("blue", "black",
  "purple", "green", "red", "yellow"))
{{< /highlight >}}

#### 引数

|名前|説明|
|:--|:--|
|**`header`**|`dashboardHeader`で生成するヘッダ|
|**`sidebar`**|`dashboardSidebar`で生成するサイドバー|
|**`body`**|`dashboardBody`で生成する本体|
|**`title`**|ブラウザのタイトルバーに表示するタイトル。`dashboardHeader`からタイトルを取ることもできます。|
|**`skin`**|色のテーマ。 "blue", "black", "purple", "green", "red", "yellow"のいずれかを選択します。|

#### 使用例

{{< highlight r >}}
## Only run this example in interactive R sessions
if (interactive()) {
# Basic dashboard page template
library(shiny)
shinyApp(
  ui = dashboardPage(
    dashboardHeader(),
    dashboardSidebar(),
    dashboardBody(),
    title = "Dashboard example"
  ),
  server = function(input, output) { }
)
}
{{< /highlight >}}

shinydashboard, version 0.6.1, License: GPL-2

### dashboardSidebar

ダッシュボードのサイドバーを生成します。ダッシュボードのサイドバーは、通常`sidebarMenu`を持ちます。そうでなければ、`sidebarSearchForm`または他のShinyの入力を持ちます。

{{< highlight r >}}
dashboardSidebar(..., disable = FALSE, width = NULL, collapsed = FALSE)
{{< /highlight >}}

#### 引数

|名前|説明|
|:--|:--|
|**`...`**|サイドバーに置く項目|
|**`disable`**|`TRUE`なら、サイドバーが無効になります。|
|**`width`**|サイドバーの幅。ピクセルを示す数値またはCSSの単位を付けた数値と文字列で指定します。|
|**`collapsed`**|`TRUE`なら、サイドバーはShiny app開始時に掴んだ状態となります。|

#### 使用例

{{< highlight r >}}
## Only run this example in interactive R sessions
if (interactive()) {
header <- dashboardHeader()

sidebar <- dashboardSidebar(
  sidebarUserPanel("User Name",
    subtitle = a(href = "#", icon("circle", class = "text-success"), "Online"),
    # Image file should be in www/ subdir
    image = "userimage.png"
  ),
  sidebarSearchForm(label = "Enter a number", "searchText", "searchButton"),
  sidebarMenu(
    # Setting id makes input$tabs give the tabName of currently-selected tab
    id = "tabs",
    menuItem("Dashboard", tabName = "dashboard", icon = icon("dashboard")),
    menuItem("Widgets", icon = icon("th"), tabName = "widgets", badgeLabel = "new",
             badgeColor = "green"),
    menuItem("Charts", icon = icon("bar-chart-o"),
      menuSubItem("Sub-item 1", tabName = "subitem1"),
      menuSubItem("Sub-item 2", tabName = "subitem2")
    )
  )
)

body <- dashboardBody(
  tabItems(
    tabItem("dashboard",
      div(p("Dashboard tab content"))
    ),
    tabItem("widgets",
      "Widgets tab content"
    ),
    tabItem("subitem1",
      "Sub-item 1 tab content"
    ),
    tabItem("subitem2",
      "Sub-item 2 tab content"
    )
  )
)

shinyApp(
  ui = dashboardPage(header, sidebar, body),
  server = function(input, output) { }
)
}
{{< /highlight >}}

shinydashboard, version 0.6.1, License: GPL-2

### sidebarMenu

ダッシュボードのサイドバーメニューとメニューの項目を生成します。`dashboardSidebar`は`sidebarMenu`を持ちます。`sidebarMenu`は`menuItem`を持ち、`menuItem`は`menuSubItem`を持ちます。

{{< highlight r >}}
sidebarMenu(..., id = NULL, .list = NULL)
{{< /highlight >}}

### menuItem

{{< highlight r >}}
menuItem(text, ..., icon = NULL, badgeLabel = NULL, badgeColor = "green",
  tabName = NULL, href = NULL, newtab = TRUE, selected = NULL,
  expandedName = as.character(gsub("[[:space:]]", "", text)),
  startExpanded = FALSE)
{{< /highlight >}}

### menuSubItem

{{< highlight r >}}
menuSubItem(text, tabName = NULL, href = NULL, newtab = TRUE,
  icon = shiny::icon("angle-double-right"), selected = NULL)
{{< /highlight >}}

#### 引数

|名前|説明|
|:--|:--|
|**`...`**|メニューの項目。`menuSubItem`で構成することもあります。|
|**`id`**|`sidebarMenu`では、`id`があると、その`id`がShinyの入力の値として用いられます。そして、どのタブが選択されているのかを示します。例えば、`id = "tabs"`の場合、`input$tabs`が現在選択されているタブの`tabName`となります。|
|**`.list`**|メニューに置く項目を含むオプションのリストで、引数`...`と同じですが、リストのフォーマットです。プログラム上で項目を生成して動作させるときに役立ちます。|
|**`text`**|メニューの項目で表示するテキスト|
|**`icon`**|`icon`で生成されるアイコンのタグ。`NULL`の場合、アイコンを表示しません。|
|**`badgeLabel`**|オプションのバッジのラベル。通常は数値、または"new"のような短い単語です。|
|**`badgeColor`**|バッジの色。有効な色は`validColors`でリストになっています。|
|**`tabName`**|メニューの項目がアクティベートするタブの名前。`href`とは両立できません。|
|**`href`**|リンクのアドレス。`tabName`とは両立できません。|
|**`newtab`**|`href`が設定されている場合に、リンクのオープンをブラウザの新しいタブで開くかどうかを指定|
|**`selected`**|`TRUE`なら、`menuItem`または`menuSubItem`が選択されて開始されます。どの項目も`selected = TRUE`でない場合、最初の`menuItem`が選択されて開始されます。|
|**`expandedName`**|各`menuItem`に与えられる固有の名前|
|**`stardExpanded`**|menuItemがShiny app開始時に展開されているかどうかを指定。`menuItems`が複数の子を持つときのみ適用可能で、子の中の1つが展開されます|

#### 詳細

メニューの項目(と同様に、サブ項目も)は、`href`または`tabName`の値を持ちます。そうでなければ、その項目は何もしません。`href`の値の場合、項目は単純に値へのリンクとなります。

`menuItem`が`NULL`でない`tabName`を持つ場合、`menuItem`はタブのような動作となります。言い換えると、`menuItem`のクリックによって`tabPanel`と同じように対応する`tabItem`が前面に出てきます。`menuItem`と`tabPanel`の違いは、`menuItem`では同じ`tabName`を持つ`tabItem`が必要ですが、`tabPanel`では`tabName`が不要である点です(`tabPanel`では、タブの名前が自動的に生成されるという構造に依るものです)。サブの項目も`tabItem`をアクティベートすることが可能です。

サブでないメニューの項目は、オプションのバッジを持ちます。バッジはテキストの上で色付けされます。

### tabItems

タブ項目のコンテナを生成します。

{{< highlight r >}}
tabItems(...)
{{< /highlight >}}

#### 引数

|名前|説明|
|:--|:--|
|**`...`**|コンテナ内に置く1つ以上の項目。項目は`tabItem`です。|

### tabItem

タブ項目のコンテナ内に置くタブを生成します。

{{< highlight r >}}
tabItem(tabName = NULL, ...)
{{< /highlight >}}

#### 引数

|名前|説明|
|:--|:--|
|**`tabName`**|タブの名前。`menuItem`または`menuSubItem`の`tabName`に対応するものでなければなりません。|
|**`...`**|タブの内容。|
