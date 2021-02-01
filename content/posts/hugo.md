---
title: "Hugo"
date: 2021-02-01T20:46:27+08:00
lastmod: 2021-02-01
author: "xiaonan"
math:
 enable: true

tags: [hugo]
categories: [hugo]
---

Hugo is one of the most popular open-source static site generators.
<!--more-->

# Basics
 
## 1 Requirements

- install `hugo`

```Bash
sudo pacman -S hugo
```

## 2 Installation

### 2.1 Create a Project

```Bash
hugo new site my_website
cd my_website
```

### 2.2 Install the Theme

```bash
git clone https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

### 2.3 Configuration
**my_website/config.toml**

```TOML
baseURL = "https://fengqigang.cn"

defaultContentLanguage = "en"

languageCode = "en"
title = "xiaonan's Blog"

theme = "LoveIt"

[params]
	version="0.2.X"

	defaultTheme = "auto"
	dataFormat = "2006-01-02"

	[parmas.app]
		title = "Xiaonan's Blog"
		noFavicon = false
		svgFavicon = ""

	[params.search]
    enable = true
    type = "lunr"
    contentLength = 4000
    placeholder = ""
    maxResultLength = 10
    snippetLength = 30
    highlightTag = "em"
    absoluteURL = false
    [params.search.algolia]
      index = ""
      appID = ""
      searchKey = ""

	[params.header]
		desktopMode = "fixed"
		mobileMode = "auto"
			
	[params.footer]	
		enable = true
		custom = ''
		hugo = true
		copyright = true
		author = true
		since = 2019

	[params.section]
		paginate = 20
		dataFormat = "01-02"
		rss = 10

	[params.list]
		paginate = 20
		dataFormat = "01-02"
		rss = 10

	[params.home]
		rss = 10
		[params.home.profile]
			enable = true
			gravatarEmail = ""
			avatarURL = "/images/avatar.png"
			title = "Xiaonan's Blog"
			subtitle = ""
			typeit = true
			social = true
			disclaimer = ""
		[params.home.posts]
			enable = true
			paginate = 6
			defaultHiddenFromHomePage = false

	[params.social]
		GitHub = "guangsizhongbin"
		Email = "guangsizhongbin@gmail.com"
		RSS = true

	[params.page]
		hiddenFromHomePage = false
		hiddenFromSearch = false
		twemoji = false
		lightgallery = false
		ruby = true
		fraction = true
		fontawesome = true
		linkToMarkdown = true
		rssFullText = false

		[parmas.page.toc]
			enable = true
			keepStatic = true
			auto = true

		[parmas.page.math]
			enable = true
			blockLeftDelimiter = ""
			blockRightDelimiter = ""
			copyTex = true
			mhchem = true

		[params.page.code]
			copy = true
			maxShowLines = 10

[menu]
	[[menu.main]]
		identifier = "posts"
		pre = ""
		post = ""
		name = "Posts"
		url = "/posts/"
		title = ""
		weight = 1

	[[menu.main]]
		identifier = "tags"
		pre = ""
		post = ""
		name = "Tags"
		url = "/Tags/"
		title = ""
		weight = 2

	[[menu.main]]
		identifier = "categories"
		pre = ""
		post = ""
		name = "categories"
		url = "/categories/"
		title = ""
		weight = 3

[markup]
	[markup.highlight]
		codeFences = true
		guessSyntax = true
		lineNos = true
		lineNumberInTable = true
		noClasses = false
	[markup.goldmark]
		[markup.goldmark.extensions]
			definitionList = true
			footnote = true
			linkify = true
			strikethrough = true
			table = true
			taskList = true
			typographer = true
		[markup.goldmark.renderer]
			unsafe = true
		[markup.tableOfContents]
			startLevel = 2
			endLevel = 6

[author]
	name = "fengxiaonan"
	email = "gaungsizhongbin@gmail.com"
	link = "fengqigang.cn"

[outputs]
	home = ["HTML", "RSS", "JSON"]
```

### 2.4 Create Post

#### 2.4.1 Setting archetypes

**my_website/archetypes/default.md**

```markdown
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
lastmod: {{ now.Format "2006-01-02"}}
author: "xiaonan"

tags: []
categories: []
featuredIamge: ""
featuredImagePreview: ""
draft: true

---
```

#### 2.4.2 Create a new website

```Bash
hugo new posts/first_post.md
```

### 2.5 Launching the Website Locally

```Bash
hugo serve
```

Go to `http://localhost:1313`

![](https://img.fengqigang.cn//img/20201013170431.png)

### 2.6 Build the Website

```Bash
hugo
```

# Markdown Syntax

## 1 Blockquotes

Add `>` before any text you want to quote:

```Markdown
> **Fusion Drive** combines a hard drive with a flash storage (solid-state drive) and presents it as a single logical volume with the space of both drives combined.
```

The rendered output looks like this:

> **Fusion Drive** combines a hard drive with a flash storage (solid-state drive) and presents it as a single logical volume with the space of both drives combined.

## 2 Task Lists

```Markdown
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media
```

The rendered output looks like this:

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

## 3. Tables

```Markdown
| Option | Description |
|--------|-------------|
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |
```

The rendered output looks like this:

| Option | Description |
|--------|-------------|
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |

## 4 Footnotes

```Markdown
This is a digital footnote[^1].
This is a footnote with "label"[^label]

[^1]: This is a digital footnote
[^label]: This is a footnote with "label"
```

This is a digital footnote[^1].
This is a footnote with "label"[^label]

[^1]: This is a digital footnote
[^label]: This is a footnote with "label"





