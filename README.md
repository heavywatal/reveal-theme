# hugo-theme-reveal: simple theme for Hugo with remark/reveal.js

## Installation

### reveal.js

https://github.com/hakimel/reveal.js

1.  Clone reveal.js
    ```sh
    git clone https://github.com/hakimel/reveal.js.git
    git -C reveal.js/ checkout tags/3.6.0
    ```

1.  Copy necessary files to `static/`:
    ```sh
    SRC=reveal.js
    DST=static/reveal.js
    rsync -auvm --exclude='theme' --exclude='*scss' $SRC/css $DST/
    rsync -auvm $SRC/js $DST/
    rsync -auvm --exclude='css' --exclude='font' $SRC/lib $DST/
    rsync -auvm --include='*/' --include='notes/notes.*' --exclude='*' $SRC/plugin $DST/
    ```

### remark

https://github.com/gnab/remark/wiki/Contributing#building

1.  Clone remark and install dependencies
    ```sh
    git clone https://github.com/hakimel/reveal.js.git
    cd remark/
    npm install
    ```

1.  Modify `package.json` to exclude highlighter from build:
    ```js
    {
      //
      "config": {
        "highlighter": false
      },
      //
    }
    ```

1.  Build remark:
    ```sh
    node make highlighter
    node make lint
    node make bundle
    node make minify
    ```

1.  Copy the minified script to `static/`:
    `cp -a out/remark.min.js ../static/`

## Options

`config.toml` of [example slides](https://heavywatal.github.io/slides/)

```toml
+++
title = "Slide decks — Heavy Watal"
theme = "reveal"
baseURL = "https://heavywatal.github.io/slides/"
buildDrafts = false
buildFuture = true
disableKinds = ["RSS", "sitemap"]
ignoreFiles = ["\\.R$", "\\.Rmd$", "\\.csv$"]
languageCode = "en-us"
noTimes = true
pygmentsUseClasses = true
pygmentsCodefences = true
googleAnalytics = "UA-***"

[author]
name = "Watal M. Iwasaki"
twitter = "@heavywatal"

[params]
og_image = "https://avatars.githubusercontent.com/heavywatal"
+++
```

Example of front matter

```toml
+++
title = "Introduction to data preprocessing"
date = 2018-03-14T16:00:00+09:00
type = "reveal"
draft = false
+++
```