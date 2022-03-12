# r2hugo

Create Hugo content from R Markdown.

r2hugo is a Hugo [theme component](https://gohugo.io/hugo-modules/theme-components/). It works alongside your normal theme and allows you to easily create content from R Markdown files.

## Install

Add r2hugo to your project as a git submodule

```
git submodule add https://github.com/thomasmarkrea/r2hugo.git themes/r2hugo
```

And update Hugo's config file, add

- `r2hugo` to `theme`
- `.rmd` to `ignoreFiles`

```
# config.toml

...

theme = ["r2hugo", ...]
ignoreFiles = [ "\\.rmd$" ]

...
```

## Usage

Use `hugo new` to create a new post.

Add the `-k` flag to tell Hugo to use the `r2hugo` archetype

```
hugo new -k r2hugo posts/test-r2hugo-post
```

This will create a new directory in `content/posts` containing `index.md` and `content.rmd`

```
content
└── posts
    └── test-r2hugo-post
        ├── index.md
        └── content.rmd
    └── ...
```

`index.md` is a standard Hugo content file, except where the content usually goes there is a [shortcode](https://gohugo.io/content-management/shortcodes/)

```
# content/posts/test-r2hugo-post/index.md

+++
title = "test-r2hugo-post"
description = "Post to test r2hugo"
categories = ['test']
tags = ['hugo', 'r']
date = 2020-01-01T13:00:00+00:00
draft = true
+++

{{% include "{{ .File.Dir }}content.md" %}}
```

`content.rmd` is where the actual content goes

````
# content/posts/test-r2hugo-post/content.rmd

---
output:
  md_document:
    variant: commonmark
---

Post to test r2hugo.

# Example Code

```{r}
print("example code")
```

# Example Plot

```{r}
plot(1:10,1:10)
```
````

To test the page, *knit* `content.rmd` and run 

```
hugo server -D
```
