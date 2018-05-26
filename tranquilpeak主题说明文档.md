---
title: "tranquilpeak主题说明文档"
date: 2018-04-29T10:49:05+08:00
lastmod: 2018-04-29T10:49:05+08:00
draft: false
keywords: []
description: ""
tags: ["hugo","主题","博客"]
categories: ["hugo"]
slug: ["tranquilpeak","theme","readme"]
author: "3mile"

# 显示左边栏
clearReading: true
# 索引页面上显示的缩略图
thumbnailImage: /cover/top.jpg
# 索引页上缩略图位置left,right,top,bottom
thumbnailImagePosition: top
#如果没有封面,自动使用默许封面
autoThumbnailImage: false
#标题位置(left center right)
metaAlignment: center
# 封面图像相对路径
coverImage: /cover/1.jpg
#封面说明内容
coverCaption: "A beautiful cover"
#标题在封面内(in),还是封面外(out)
coverMeta: in
# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial
---

<!-- toc -->

### 语言配置

只需编辑以下值`config.{toml,yaml,json}`：

```
defaultContentLanguage = “ en-us ”
```

由以下代码之一（代码介于`()`）之间：

- 中文（`zh-cn`）
- 中文繁体（`zh-tw`）
- 英语（`en-us`）
- 德语（`de-de`）
- 法语（`fr-fr`）
- 日语（`ja`）
- 葡萄牙语（`pt-br`）
- 俄语（`ru`）
- 西班牙语（`es`）
- 越南语（`vi`）

如果您的语言不可用，请遵循此准则（例如：添加瑞典语（`sv-se`））：

1. 设置`defaultContentLanguage`为`sv-se`Hugo配置文件`config.{toml,yaml,json}`
2. `sv-se.yaml`在`theme/tranquilpeak/i18n/`文件夹中创建文件
3. 复制`theme/tranquilpeak/i18n/en-us.yaml`并粘贴到`sv-se.yml`文件的内容
4. 在瑞典语中用英语翻译替换所有英文字符串

#### 菜单翻译

菜单使用Hugo菜单定义<https://gohugo.io/extras/menus/>

您可以通过设置`identifier`与翻译键相匹配的翻译菜单条目。通过这种方式，`name`根本不会被使用。

### 为Tranquilpeak设置默认主题

`config.{toml,yml,json}`通过将`theme`变量更改为，修改主题`tranquilpeak`

### 定义日期格式

默认情况下，打印日期将如下所示：`mmmm d, yyyy`例如：“2006年1月2日”

您可以通过设置进行自定义

```yaml
[params]
  dateFormat = "2 January 2006"
```

将产生：“2006年1月2日”

注意：日期格式应该遵守`go` `Time`包语法，请参阅<https://golang.org/pkg/time/>

**此外，如果您使用完全命名的月份（不支持“jan”，“feb”等简短命名月份），则会翻译月份。**

例：

```yaml
defaultContentLanguage = “ fr-fr ”
```

“2006年7月21日”将输出“21 Juillet 2006”。

### 定义全局关键字

您可以为搜索引擎定义关键字。这些关键字将被添加到所有页面上。

```
[ params ]
   keywords = [ “ development ”，“ next-gen ” ]
```

### 主题配置

备份您的配置：

```bash
cp config.{toml,yml,json} config.{toml,yml,json}.backup 
```

复制示例配置

```bash
cp themes/tranquilpeak/exampleSite/config.toml .
```

填写`config.toml`您的信息。阅读以上章节以获取更多信息。

#### 侧边栏

侧边栏功能强大且易于配置。您可以根据需要添加多组链接和链接。

```yaml


[[menu.main]]
  weight = 0
  identifier = "home"
  name = "Home"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-home\"></i>"
  url = "/"
[[menu.main]]
  weight = 1
  identifier = "categories"
  name = "Categories"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-bookmark\"></i>"
  url = "/categories"
[[menu.main]]
  weight = 2
  identifier = "tags"
  name = "Tags"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-tags\"></i>"
  url = "/tags"
[[menu.main]]
  weight = 3
  identifier = "archives"
  name = "Archives"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-archive\"></i>"
  url = "/archives"
[[menu.main]]
  weight = 4
  identifier = "search"
  name = "Search"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-search\"></i>"
  url = "/#search"
  class = "st-search-show-outputs"
[[menu.main]]
  weight = 4
  identifier = "about"
  name = "About"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-question\"></i>"
  url = "/#about"

[[menu.links]]
  weight = 0
  identifier = "github"
  name = "GitHub"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-github\"></i>"
  url = "https://github.com/kakawait"
[[menu.links]]
  weight = 1
  identifier = "stackoverflow"
  name = "Stack Overflow"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-stack-overflow\"></i>"
  url = "https://stackoverflow.com/users/636472/kakawait"

[[menu.misc]]
  weight = 0
  identifier = "rss"
  name = "RSS"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-rss\"></i>"
  url = "/index.xml"
```
| 变量       | 描述                     | 类型          |
| ---------- | ------------------------ | ------------- |
| weight     | 菜单按weight值排序       | INT           |
| identifier | 识别的唯一标识符         | string        |
| name       | 要显示的标题             | string        |
| pre        | 图标显示在名称的左侧     | template.HTML |
| url        | 菜单网址                 | string        |
| class      | 添加到`a`链接标记的CSS类 | string        |

`identifier`可以用于翻译，参见[菜单翻译](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md#menu-translation)。

#### Header

标题的链接是可定制的。您可以在标题的右侧添加链接（作为图标），而不是作者的gravatar图片或作者的图片。默认情况下，显示作者的gravatar或作者的图片。

例如，要显示打开algolia搜索窗口的快捷方式：

| Variable | Description                                            |
| -------- | ------------------------------------------------------ |
| url      | URL链接。如果URL是内部的，则域名不是必需的             |
| icon     | 调用外部图标库 [awesome](http://fontawesome.io/icons/) |
| class    | 添加到链接的CSS类                                      |

#### Author

```
[author]
  name = "3mile"
  bio = "个人简介 **酷**"
  job = "苦逼码家"
  location = "中国.成都"
  # 您的Gravatar电子邮件。在博客的任何地方覆盖`author.picture` 
  gravatarEmail = "thibaud.lepretre@gmail.com"
  # 您的个人资料图片
  # 如果填写了Email的话,个人图片会被覆盖
  picture = "https://cdn1.iconfinder.com/data/icons/ninja-things-1/1772/ninja-simple-512.png"
  # 你的Twitter用户名没有@ 如：tranquilpeak
  twitter = "thibaudlepretre"
  # 你的谷歌加profile id。例如：+ ThibaudLepretre或114625208755123718311
  googlePlus = "+ThibaudLepretre"
```

| Variable      | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| name          | 作者的名字                                                   |
| gravatarEmail | Email地址,如果填写,则你的图片会被覆盖                        |
| bio           | 你的个人传记  （支持Markdown和HTML）                         |
| job           | 你的工作                                                     |
| location      | 你的地区                                                     |
| picture       | 你的照片(或者图片)                                           |
| twitter       | Your Twitter username without the @. E.g : `thibaudlepretre` |
| googlePlus    | Your google plus profile id. E.g : `+ThibaudLepretre` or `114625208755123718311` |

#### Customization

**注意**并非所有的定制都记录在这里，您可以签出[示例config.toml](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/exampleSite/config.toml)。

```yaml
[params]
  sidebarBehavior = 1
  thumbnailImage = true
  thumbnailImagePosition = "right"
  autoThumbnailImage = true
  coverImage = "cover.jpg"
  favicon = /favicon.png
  imageGallery = true
  hierarchicalCategories = true
  syntaxHighlighter = 'highlight.js'
```

| 变量                                                     | 描述                                                         |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| sidebarBehavior                                          | 定义标题和侧边栏的行为：1：在超大屏幕上显示超大的侧边栏，在大屏幕上显示大型侧栏，在中型屏幕上显示中型侧栏，在小屏幕上显示标题栏，点击打开按钮时在特大屏幕上显示特大型侧栏，在所有下部屏幕上显示大型侧栏。 （默认）2：在特大屏幕和大屏幕上显示大型侧栏，在中型屏幕上显示中等侧栏，在小屏幕上显示标题栏，并在单击打开按钮时滑动大型侧栏3：点击打开按钮时，在大屏幕和中屏幕上显示媒体侧栏，在小屏幕和中型侧栏上显示标题栏。4：在所有屏幕上显示标题栏，在特大屏幕上滑动超大侧栏，在所有下屏幕上滑动大侧栏5：在所有屏幕上显示标题栏，并在大屏幕上滑动大型侧栏6：所有屏幕上的isplay标题栏和中等侧栏都会被刷新 |
| clearReading                                             | 在所有文章页面隐藏侧边栏，让文章充分展现阅读效果，欣赏宽广的图片和封面图片。无用，如果`sidebarBehavior`等于`3`或`4`。（true：启用，false：禁用）。默认行为：`params.clearReading`主题配置文件中的值。 |
| thumbnailImage                                           | 在索引页面上显示每篇文章的缩略图                             |
| thumbnailImagePosition                                   | 在标题中的索引页（右显示缩略图图像`right`，`left`或`bottom`）。将此值设置为`right`如果您有旧帖子以保留旧样式并`thumbnailImagePosition`在帖子上定义以覆盖此设置。（默认值：`right`） |
| autoThumbnailImage                                       | 如果没有缩略图图像作为缩略图图像，自动选择封面图像或帖子图库中的第一张图片。将该值设置为`true`，如果你有使用的封面图片或第一张照片的缩略图，并设置旧帖子`autoThumbnailImage`到`false`上个帖子覆盖此设置。（默认值：`true`） |
| 封面图片                                                 | 您的博客封面图片。**我强烈建议您使用CDN来加快页面的加载速度。有许多像Cloudinary这样的免费CDN，或者您也可以间接使用Google Photos等服务。** |
| 图标                                                     | 你的图标路径（默认值：`/favicon.png`）                       |
| imageGallery                                             | 在帖子结尾处显示包含`photos`变量的图片库。（false：禁用，true：启用） |
| hierarchicalCategories                                   | 定义类别将在父母之间建立层次结构：`categories = ["foo", "bar"]`将“条”视为“foo”的子类别。如果为假，它将平分类别。 |
| customCSS（*DEPRECATED请参阅使用配置添加自定义JS或CSS*） | 使用css定义文件来覆盖或扩展主题css：`customCSS`= [“css / mystyles.css”]。 |
| customJS（*请参阅使用配置添加自定义JS或CSS*）            | 用js定义覆盖或扩展主题js：`customJS`= [“js / myscripts.js”]的文件。 |
| SyntaxHighlighter的                                      | 在`highlight.js`和之间定义要使用的语法突出显示器（如果未设置语法突出显示禁用）`prism.js` |

##### 使用配置添加自定义JS或CSS

如果你需要添加一些额外的JavaScript或CSS文件到你的博客而不分叉或覆盖主题本身，你可以使用下面的配置：

```
[params]
  [[params.customJS]]
    src = "https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.8.0/languages/go.min.js"
    integrity = "sha256-LVuWfOU0rWFMCJNl1xb3K2HSWfxtK4IPbqEerP1P83M="
    crossorigin = "anonymous"
    async = true
    defer = true

  [[params.customJS]]
    src = "https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.8.0/languages/dockerfile.min.js"
    integrity = "sha256-putofyQv7OB569xAldpyBnHJ0Uc+7VGp5Us05IgDGss="
    crossorigin = "anonymous"
    async = true
    defer = true

  [[params.customJS]]
    src = "js/myscript.js"

  [[params.customCSS]]
    href = "css/mystyle.css"
```

**注意**，关键结构没有限制，每个键将被转换为标签属性。

此外，即使前面的语法仍然支持（`customJS = ["js/myscripts.js"]`），您不能混合使用新旧语法。

#### 综合服务

```
disqusShortname =
googleAnalytics = 
```

```
[author]
  gravatarEmail =
```

```
[params]
  fbAdminIds = 
  fbAppId = 
```

| Variable        | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| disqusShortname | 你的Disqus短名。                                             |
| gravatarEmail   | 你的gravatar电子邮件。                                       |
| googleAnalytics | 你的 Google analystics web property ID : UA-XXXXX-X          |
| fbAdminIds      | 您的Facebook用户ID用于将您的博客与您的Facebook用户帐户（Facebook Insights）连接起来。使用数组语法。例如：`[9830047, 1003342]`。访问[Facebook文档](https://developers.facebook.com/docs/platforminsights/domains)以获取更多信息。 |
| fbAppId         | 您的Facebook应用ID用于将您的博客与Facebook应用帐户（Facebook Insights）关联起来。例如：`9841307`。访问[Facebook文档](https://developers.facebook.com/docs/platforminsights/domains)以获取更多信息。 |

#### 共享选项

```
[params]
  [[params.sharingOptions]]
    name = "Facebook"
    icon = "fa-facebook-official"
    url = "https://www.facebook.com/sharer/sharer.php?u=%s"

  [[params.sharingOptions]]
    name = "Twitter"
    icon = "fa-twitter"
    url = "https://twitter.com/intent/tweet?text=%s"

  [[params.sharingOptions]]
    name = "Google+"
    icon = "fa-google-plus"
    url = "https://plus.google.com/share?url=%s"
```

您可以评论并取消注释以启用或禁用共享选项。如果您有自己的分享选项，只需在您的配置上添加新的分享选项。例如与**foo_bar**社交网络：

```
[params]
  [[params.sharingOptions]]
    name = "Foo bar"
    icon = "fa-foo-bar"
    url = "https://www.foo-bar.com/sharer/sharer.php?u=%s"
```

| Variable | Description                                                  |
| -------- | ------------------------------------------------------------ |
| name     | 您分享网站的名称。                                           |
| icon     | Name of the fontawesome icon class (Go to [font-awesome icons](http://fontawesome.io/icons/) to find class name of icon) |
| url      | 链接的URL。使用％s来指定永久链接的位置。                     |

#### 启用页面

Tranquilpeak为您提供2页显示标签，按类别，按日期和关于页面的所有帖子标题和日期。要启用其中一个网页，只需添加以下[分类标准](https://gohugo.io/taxonomies/overview/)：

```
[ categories ]
   tag = “ tags ”
   category = “ categories ”
```

## 综合业务配置

### 谷歌分析

#### 在撰写文章时排除主机名（localhost）

在您撰写文章时，您需要在部署您的网站之前多次检查结果。如果您启用了Google分析服务，Google即使在主机名为本地主机时也会包含所有已完成的请求，这可能会大大扭曲结果。为了克服这个问题，您必须在Google Analytics网站上添加一个过滤器。

按照以下步骤添加新的过滤器：

1. 登录到您的Google Analytics帐户
2. 选择**管理**标签，然后导航至**属性**要在其中创建过滤器**（帐户>属性>查看）**
3. 在“ **查看”**列中，点击“ **过滤器”**按钮
4. 点击**+ NEW FILTER**按钮
5. 输入过滤器的名称
6. 选择**自定义过滤器**，**过滤器字段**：`Hostname`，**过滤器模式**： `(.*?localhost.*?)`
7. 点击**保存**按钮

## 快速和简单的修改

### 先决条件

由于您要编辑主题，因此必须安装修改后所需的所有必要工具：[安装](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/developer.md#installation)

**在主题文件夹中运行命令： hexo-blog/themes/tranquilpeak**

### 改变全球风格

如果您想更改字体系列，字体大小，侧边栏颜色等等，请查看`source/scss/utils/_variables.scss`文件。这个文件包含在这个主题中使用的全局变量。**修改后构建主题以查看更改。**

### 更改代码着色（Highlight.js主题）

Tranquilpeak整合了GitHub启发的自己的highlight.js主题。当然，您可以用highlight.js存储库中的其他主题来替换它。由于Hexo使用不同的CSS类名，所有的主题都没有准备就绪，但它们很容易兼容。

按着这些次序 ：

1. 在这里获得您的主题：[Highlight.js主题](https://github.com/isagalaev/highlight.js/tree/master/src/styles)或创建您的[主题](https://github.com/isagalaev/highlight.js/tree/master/src/styles)
2. 遵循`src/scss/themes/hljs-custom.scss`文件中的准则
3. 用`npm run prod`or 构建主题`grunt buildProd`。了解更多关于Grunt任务：[Grunt任务](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak/blob/master/docs/developer.md#grunt-tasks)

## 写文章

要撰写文章，您必须使用Markdown语言。[在这里](https://guides.github.com/features/mastering-markdown/#examples)您可以找到Markdown语法的主要基础知识。
请注意，有许多不同版本的Markdown，其中一些不支持Hugo。

**我强烈建议您使用CDN来加快页面的加载速度。有许多像Cloudinary这样的免费CDN，或者您也可以间接使用Google Photos等服务。**

### 前置设置

Tranquilpeak引入了新的变量，给你很多可能性。
```yaml
disqusIdentifier: fdsF34ff34
keywords:

- javascript
- hexo
clearReading: true
thumbnailImage: image-1.png
thumbnailImagePosition: bottom
autoThumbnailImage: yes
metaAlignment: center
coverImage: image-2.png
coverCaption: "A beautiful sunrise"
coverMeta: out
coverSize: full
coverImage: image-2.png
gallery:
    - image-3.jpg "New York"
    - image-4.png "Paris"
    - http://i.imgur.com/o9r19kD.jpg "Dubai"
    - https://example.com/orignal.jpg https://example.com/thumbnail.jpg "Sidney"
comments: false
showTags: true
showPagination: true
showSocial: true
showDate: true
```
| 变量                   | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| disqusIdentifier       | 定义用于在Disqus系统中查找页面线程的唯一字符串。             |
| keywords               | 为搜索引擎定义关键字。您还可以在Hugo配置文件中定义全局关键字。 |
| clearReading           | 在所有文章页面隐藏侧边栏，让文章充分展现阅读效果，欣赏宽广的图片和封面图片。无用，如果`params.sidebarBehavior`等于`3`或`4`。（true：启用，false：禁用）。默认行为：`params.clearReading`主题配置文件中的值。 |
| autoThumbnailImage     | 如果没有缩略图图像作为缩略图图像，自动选择封面图像或帖子图库中的第一张图片。`autoThumbnailImage`覆盖`autoThumbnailImage`主题配置文件中的设置 |
| thumbnailImage         | 图像显示在索引视图中。                                       |
| thumbnailImagePosition | 在标题中的索引页（右显示缩略图图像`right`，`left`或`bottom`）。`thumbnailImagePosition`覆盖`thumbnailImagePosition`主题配置文件中的设置 |
| metaAlignment          | 元（标题，日期和类别）对齐方式（右侧，左侧或中间）。默认行为：向左 |
| cover                  | 图片以帖子视图的文章顶部全尺寸显示。如果未配置缩略图图像，则封面图像也会用作缩略图图像。查看这里的美丽演示：[封面图像演示](https://tranquilpeak.kakawait.com/2015/05/cover-image-showcase/) |
| coverSize              | `partial`：封面图片占据屏幕高度的一部分（60％）`full`，：封面图片占整个屏幕的高度。 |
| coverCaption           | 在封面图片下添加标题：[封面标题演示](https://tranquilpeak.kakawait.com/2015/05/cover-image-showcase/) |
| coverMeta              | `in`：在封面图像上显示后期元（标题，日期和类别）`out`，：照常在封面图像下显示元（标题，日期和类别）。默认行为：`in` |
| comments               | 在帖子末尾的图片库（带有fancybox）中显示的图像。如果未配置缩略图图像并且也会覆盖图像，则会将第一张照片用作缩略图图像。格式：`original url [thumbnail url] [caption]`例如：`https://example.com/original.jpg https://example.com/thumbnail.jpg "New York"` |
| 注释                   | `true`：显示帖子的评论。                                     |
| showdate相似           | `true`：显示日期`true`（默认）                               |
| showTags               | `true`：显示此页面的标签。                                   |
| showPagination         | `true`：显示分页。                                           |
| showSocial             | `true`：显示社交按钮，例如Twitter，Facebook上的分享...       |
| showMeta               | `true`：显示帖子meta（日期，类别）。                         |
| showActions            | `true`：显示帖子操作（导航，共享链接）。                     |

示例：索引页上的帖子将如下所示：`thumbnailImagePosition`set to `bottom`：

示例：索引页上的帖子将如下所示：`thumbnailImagePosition`set to `bottom`：
[![缩略图图像位置底](/assets/readme/1.jpg)]

与之相同：`thumbnailImagePosition`设置为`right`：
[![缩略图图像位置向右](/assets/readme/2.jpg)]

与之相同：`thumbnailImagePosition`设置为`left`：
[![缩略图图像位置左](/assets/readme/3.jpg)]

### 定义帖子摘录

使用：

- `<!--more-->` 定义帖子摘录并在帖子内容中保留帖子摘录

### 显示目录

随着帖子摘录功能启用`<!--more-->`评论，

您可以使用显示帖子内容的目录 `<!-- toc -->`。将此注释放置在要显示内容表的位置。

以下是生成的目录：
[![缩略图图像位置左](/assets/readme/4.jpg)]

### 标签

Tranquilpeak引入新的标签来显示警报消息，全幅图像并创建美丽的画廊。

### alert
[![警告标签](/assets/readme/5.jpg)]

例如：

{{< alert danger no-icon >}}
Here is a danger alert without icon
{{< /alert >}}

| Argument | Description                      |
| -------- | -------------------------------- |
| Classes  | . info |
|          | . succes                          |
|          | . warning                         |
|          | . danger                          |
|          | . no-icon                        |

#### Highlight Text

![highlight_text-tag](https://s3-ap-northeast-1.amazonaws.com/tranquilpeak-hexo-theme/docs/1.6/highlight_text-tag.png)

Highlight text tag is useful to highlight an interesting part in a text. Check it live here : [Highlight text tag demo](https://tranquilpeak.kakawait.com/2014/10/tags-plugins-showcase/#highlight-text)

Syntax:
```
{{< hl-text classes >}}
content
{{< /hl-text >}}
```

E.g:  
```
{{< hl-text danger >}}
your highlighted text
{{< /hl-text >}}
```

| Argument | Description                                                  |
| -------- | ------------------------------------------------------------ |
| Classes  | redgreenbluepurpleorangeyellowcyanprimarysuccesswarningdanger |
|          | green                                                        |
|          | blue                                                         |
|          | purple                                                       |
|          | orange                                                       |
|          | yellow                                                       |
|          | cyan                                                         |
|          | primary                                                      |
|          | success                                                      |
|          | warning                                                      |
|          | danger                                                       |

**将包含高亮文本标签的段落放在里面很重要，** `<p>...</p>` **否则以下内容可能无法呈现。**

#### 图片

图像标签对添加图像和创建美丽的画廊很有用。检查这里有什么可能：[图片标签演示](https://tranquilpeak.kakawait.com/2014/10/tags-plugins-showcase/#image)

语法：

Syntax:
```
{{< image classes="[classes]" src="[/path/to/image]" thumbnail="[/path/to/thumbnail]" group="[group-name]" thumbnail-width="[width of thumbnail]" thumbnail-height="[height of thumbnail]" title="[title text]" >}}
```

E.g:
```
{{< image classes="fancybox right clear" src="image2.png" thumbnail="http://google.fr/images/image125.png" group="group:travel" thumbnail-width="150px" thumbnail-height="300px" title="A beautiful sunrise" >}}
```


| Argument                    | Description                                                  |
| --------------------------- | ------------------------------------------------------------ |
| classes (optional)          | 你可以添加CSS类来风格化图像。用空格分隔课程。Tranquilpeak集成了许多css类来创建好的效果：  <ul><li><strong>fancybox</strong> :  生成fancybox图像。</li><li><strong>nocaption</strong> :  图像的标题不会显示。</li><li><strong>left</strong> :  图像将在左侧浮动。</li><li><strong>right</strong> : 图像将在右侧浮动。</li><li><strong>center</strong> :  图像将在中心。</li><li><strong>fig-20</strong> :  图像占用宽度宽度的20％，并自动浮动在左侧。</li><li><strong>fig-25</strong> :  图像占用宽度的25％，并自动浮动在左侧。</li><li><strong>fig-33</strong> :  图像占用宽度的33％，并自动浮动在左侧。</li><li><strong>fig-50</strong> :  图像占用后宽度的50％，并自动浮动在左侧。</li><li><strong>fig-75</strong> :  图像将占用后宽度的75％，并自动浮动在左侧。</li><li><strong>fig-100</strong> :  图像将占用后宽度的100％。</li><li><strong>clear</strong> : Add a div with `clear:both;`  在图像之后添加样式附加的div 以检索帖子的正常流程。</li></ul> |
| group (optional)            | 一个组的名称，用于创建一个画廊。**仅适用于带有fancyboxCSS类的图像** |
| src                         | 原始图像的路径。                                             |
| thumbnail (optional)        | 缩略图图像的路径。如果为空，则会显示原始图像。               |
| thumbnail-width (optional)  | 宽度缩略图图像。如果缩略图图像为空，则宽度将附加到从原始图像创建的缩略图图像上。例如：`150px`或`85%`。 |
| thumbnail-height (optional) | 缩略图图像的高度。如果缩略图图像为空，则高度将附加到从原始图像创建的缩略图图像上。例如：`300px`或`20%`。 |
| title (optional)            | 图像下标题显示的图像标题。`Alt`HTML属性将使用这个标题。例如：`"A beautiful sunrise"`。 |

#### 选项卡式代码块

选项卡式代码块可用于对多个相关的代码块进行分组。例如，Web组件的源代码（html，css和js）。或者比较不同语言的源代码。

![tabbed_codeblock-tag](/assets/readme/6.jpg)

Check it live : [tabbed code block demo](https://tranquilpeak.kakawait.com/2014/10/tags-plugins-showcase/#tabbed-code-block)

Syntax:

```js
{{< tabbed-codeblock name link >}}
    <!-- tab lang -->
        source code
    <!-- endtab -->
{{< /tabbed-codeblock >}}
```

E.g:  
``` js
{{< tabbed-codeblock example 网址 >}}
    <!-- tab js -->
        var test = test;
    <!-- endtab -->
    <!-- tab css -->
        .btn {
            color: red;
        }
    <!-- endtab -->
{{< /tabbed-codeblock >}}
```


| Argument        | Description              |
| --------------- | ------------------------ |
| Name (optional) | 代码块的名称或文件的名称 |
| Link (optional) | 链接到演示或文件         |
| Lang (optional) | 编程语言用于当前选项卡   |

#### 宽幅图像

宽幅图像标签有助于全宽显示宽幅图像。它占用整个窗口宽度。检查结果：[宽幅图像标签演示](https://tranquilpeak.kakawait.com/2014/10/tags-plugins-showcase/#wide-image)

Syntax:

```
{{< wide-image src="'/path/to/image'" title="'title text'" >}}
```

E.g:
```
{{< wide-image src="http://google.fr/images/image125.png" title="A beautiful sunrise" >}}
```


| Argument         | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| src              | 原始图像的路径。                                             |
| title (optional) | 图像下标题显示的图像标题。`Alt`HTML属性将使用这个标题。例如：`"A beautiful sunrise"`。 |

## 编写页面

有时候，你需要创建一个**页面**是**不是**一个**普通的博客文章**，在这里你要隐藏的日期，社交分享按钮，标签，类别和分页。例如博客页面“ *关于”*或“ *联系人”*就是这种情况，不需要对其进行时间戳（也不标记或分类），也不提供分页，也不打算在社交网络上共享。

为了创建这样一个页面，你可以这样做：

```
hugo new page/contact.md
```

这将`contact.md`在`content/page` 预填充的目录中创建以下前端内容中的文件。

```yaml
---
title: "New Page"
categories:
- category
- subcategory
tags:
- tag1
- tag2
keywords:
- tech
comments:       false
showMeta:       false
showActions:    false
#thumbnailImage: //example.com/image.jpg
---

```

The rest is basically the same as for a regular _[post](#writing-posts)_.

## Running

Run `hugo server` and start writing! :)
