This repository is a customized version of the Hexo theme Shoka.

It is based on the original work by amehime and modified mainly for personal use,
including adjustments to layout, styles, and minor functionality to better fit
my own blogging workflow.

This project is not intended to be a full replacement for the original theme.
For the original implementation, please refer to:
https://github.com/amehime/hexo-theme-shoka

The original project is licensed under the MIT License.
All credit for the original design and implementation goes to amehime.

# Usage
- clone
- update `theme` fragment as `shoka-custom`
- Install the necessary plugins
  - [hexo-renderer-multi-markdown-it](https://www.npmjs.com/package/hexo-renderer-multi-markdown-it)
  - [hexo-autoprefixer](https://www.npmjs.com/package/hexo-autoprefixer)
  - [hexo-algoliasearch](https://www.npmjs.com/package/hexo-algoliasearch)
  - [hexo-symbols-count-time](https://www.npmjs.com/package/hexo-symbols-count-time)
  - [hexo-feed](https://www.npmjs.com/package/hexo-feed)

There is a recommended configuration for hexo config:
```yaml
markdown:
  render: # 渲染器设置
    html: true # 允许 HTML 标签。
    xhtmlOut: true # 使用 '/' 来闭合单标签 （比如 <br />）。
    breaks: true # 转换段落里的 '\n' 到 <br>。
    linkify: true # 将类似 URL 的文本自动转换为链接。
    typographer: 
    quotes: '“”‘’'
  plugins: # markdown-it 插件设置
    - plugin:
        name: markdown-it-toc-and-anchor # 文章目录与锚点插件
        enable: true
        options: # 文章目录以及锚点应用的 class 名称，shoka 主题必须设置成这样
          tocClassName: 'toc'
          anchorClassName: 'anchor'
    - plugin:
        name: markdown-it-multimd-table # 多功能表格插件
        enable: true
        options:
          multiline: true
          rowspan: true
          headerless: true
    - plugin:
        name: ./markdown-it-furigana # 假名插件
        enable: false
        options:
          fallbackParens: "()"
    - plugin:
        name: ./markdown-it-spoiler # 隐藏文本插件
        enable: true
        options:
          title: "我不是隐藏文本"

# 文件压缩
minify:
  html:
    enable: true
    exclude: # 排除 hexo-feed 用到的模板文件
      - '**/json.ejs'
      - '**/atom.ejs'
      - '**/rss.ejs'
  css:
    enable: true
    exclude:
      - '**/*.min.css'
  js:
    enable: false
    mangle:
      toplevel: true
    output:
    compress:
    exclude:

autoprefixer:
  exclude:
    - '*.min.css'

algolia:
  appId: 
  apiKey: 
  adminApiKey: 
  chunkSize: 5000
  indexName: 
  fields:
    - title #必须配置
    - path #必须配置
    - categories #推荐配置
    - content:strip:truncate,0,50000
    - gallery
    - photos
    - tags

feed:
    limit: 20
    order_by: "-date"
    tag_dir: false
    category_dir: false
    rss:
        enable: true
        template: "themes/shoka/layout/_alternate/rss.ejs"
        output: "rss.xml"
    atom:
        enable: true
        template: "themes/shoka/layout/_alternate/atom.ejs"
        output: "atom.xml"
    jsonFeed:
        enable: true
        template: "themes/shoka/layout/_alternate/json.ejs"
        output: "feed.json"
```

# Modifications
- Disable ruby, polyfill, valine, quicklink, lazyload, exturl, instantsearch functionalities, titletime
- Disable copyright info copying
- Customize header file

ruby is for furigana in Japanese text, which is not needed here, and may cause rendering issues on KaTeX pages.
polyfill is not needed now, and may cause warnings in console.
valine is a comment system that I do not use.
quicklink will cause unexpected password prompt on some pages. Since I enabled nginx authentication
lazyload causes issues when using custom HTML tags.
exturl is not needed.

copyright will make copying text troublesome.
