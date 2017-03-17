# ![presskit.html](header.png)

> Static re-implementation of presskit()

![Build status](https://travis-ci.org/pixelnest/presskit.html.svg?branch=master)
[![Standard - JavaScript Style Guide](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

* [Why presskit.html](#why)
* [Roadmap](#roadmap)
* [Installation](#installation)
* [Usage](#usage)
* [Documentation](#documentation)
* [Migration Guide](#migration-guide)
* [Credits](#credits)

_Created by [Pixelnest Studio](http://pixelnest.io/)._

This is a complete re-implementation, with a permissive MIT license, of [presskit()][dopresskit], which was originally created by [Rami Ismail](https://twitter.com/tha_rami) of [Vlambeer](http://www.vlambeer.com).

---

**presskit.html** is a tool to create a presskit for your company, products or games.

To quote the original [presskit()][dopresskit]:

> Developers & press both have the same goal: to bring great games to as many people as possible - after all, a good game is worth nothing if no-one plays it. For the press, finding out about a game but not having access to information & media for the game means that they can't write about it. Of course, developers want to spend their valuable time making games instead of press pages.

> **presskit()** (pronounced _'do presskit'_) is the solution. Free for everyone, open and easy-to-use for both developers & press. Developers only have to spend an hour or so creating well-laid out press pages with everything the press needs to write to their hearts desire. Everybody wins.

It uses an **almost-identical format and output** as its precursor. The goal is to be compatible, as much as possible.

And even if [presskit()][dopresskit] was conceived with videogames in mind, we think that you can use it for any kind of product.

Examples:

* [Pixelnest Studio](http://pixelnest.io/presskit/)
* [Vlambeer](http://www.vlambeer.com/press/)
* [Flying Oak Games](http://www.flying-oak.com/presskit/index.php)
* [Chucklefish](http://chucklefish.org/cf-presskit/index.php)

The goal of **presskit.html** is to generate only static HTML pages — no PHP required at all. Just fill some XML data files, add some images, execute a command, and boom. It's done.

**You already have a presskit and you want to use this tool instead of the old un-maintained PHP-based [presskit()][dopresskit]? [Read the migration guide](#migration-guide).**

## Why

**Why reimplement [presskit()][dopresskit]?** We love the concept behind static site generators like [Jekyll](https://jekyllrb.com) or [Hugo](https://gohugo.io). These tools create lightweight static HTML pages, which are, by design, more secure and efficient than using a PHP server, for example.

Moreover, if you use one of these tools to build your company or product's website, you can simply drop the result of **presskit.html** into your site directly — it's just HTML pages, after all. 😉

We have also added some nice little things (like a "Press Copy Request" button, or widgets integration) and created a more robust implementation of [presskit()][dopresskit] (which is, unfortunately, un-maintained since 2014).

However, _we have tried to be as close as possible to the original presskit format and style._ In fact, comparing the output of **presskit.html** with the one of [presskit()][dopresskit] should be almost indistinguishable.

This is by design: the aim of the original [presskit()][dopresskit] was to create an instantly-recognizable website — almost a standard in the videogame industry.

Just try it: [follow our migration guide](#migration-guide), run **presskit.html** in the folder containing your [presskit()][dopresskit]-based `data.xml` and `images/` and you will have a ready to deploy set of HTML pages which are almost identical to what you already have.

## Roadmap

The roadmap is available on [Trello](https://trello.com/b/5T6BIyi3/open-source-presskit-html).

## Installation

The simplest way to install **presskit.html** is to use [npm](http://npmjs.org/):

```shell
npm install -g <TODO,  package not ready!>
```

(Feeling fancy? Use [Yarn](https://yarnpkg.com/en/) instead.)

This should add a globally available `presskit` command to your shell.

## Usage

Run this command:

```
presskit build
```

**presskit.html** will then scan your local working directory (where you are executing the command) and all direct sub-directories for `data.xml` files and `images/` folders.

You can also specify the folder to scan:

```shell
presskit build path/to/folder
```

The `presskit` command does a bunch more (watch mode, generation of `data.xml`, etc.). Use `presskit -h` to learn more.

In order to generate a complete presskit, you should have:

- One `data.xml` for your company.
- One `data.xml` per product in unique subfolders.
- All assets (mostly images) located in an `images/` subfolder next to the corresponding `data.xml`.

Example:

```
📄 data.xml
📂 images/
  📄 header.png
  📄 logo.png
📂 product-name-01/
  📄 data.xml
  📂 images/
    📄 header.png
    📄 logo.png
    📄 screenshot1.png
    📄 screenshot2.png
```

The `header.png` is used as the banner for the corresponding page. `logo.png` will be used as the product's brand.

The arborescence above should generate a build folder containing:

```
📂 build/
  📄 index.html
  📂 images/
    📄 header.png
    📄 logo.png
    📄 images.zip
    📄 logo.zip
  📂 product-name-01/
    📄 index.html
    📂 images/
      📄 header.png
      📄 logo.png
      📄 screenshot1.png
      📄 screenshot2.png
      📄 images.zip
      📄 logo.zip
  📂 css/
  📂 js/
```

Simply copy **all** the files in the `build/` folder to your server… and you're done!

_Note: the webserver is **not** included._

You can also [try our example](https://github.com/pixelnest/presskit.html/tree/master/data) from this repository.

## Documentation

TODO

## Migration Guide

This tool is almost a drop-in replacement for [presskit()][dopresskit] (well, except for the fact that it generates HTML instead of using a PHP back-end — but that's simpler, not harder). Which mean that you can go in your folder containing the `data.xml` and `images/`, run `presskit build` and boom, you're done.

_Well, almost._

We have made some breaking changes between this format and the original [presskit()][dopresskit] format. But be reassured: they are fairly small, and are, indeed, useful.

Follow the guide.

### URLs

This re-implementation of [presskit()][dopresskit] has a big difference: all your product URLs will break. With [presskit()][dopresskit], you pointed to `/sheet.php?p=MYSUPERGAME` for the `MYSUPERGAME` page. Here, you will point to `/MYSUPERGAME/` directly (the `index.html` is not required, which makes prettier URLs).

**This can't be changed.** We don't use PHP, but simple, robust and lightweight HTML files, and this difference is inevitable.

### External URLs

[presskit()][dopresskit] didn't require the protocol (ie., `http` or `https`) for most URLs in the `data.xml`.

For example:

```xml
<socials>
  <social>
    <name>twitter.com/pixelnest/</name>
    <link>twitter.com/pixelnest/</link>
  </social>
</socials>
```

Note that the `<link>` has no `http` or `https` protocol before its destination.

The problem with that is that we cannot deduce the protocol automatically. It will work seamlessly for the biggest sites like Facebook or Twitter, but we cannot guarantee that it will link correctly for everything.

That's why we require that you specify the protocol for your URLs:

```xml
<socials>
  <social>
    <name>twitter.com/pixelnest/</name>
    <link>https://twitter.com/pixelnest/</link>
  </social>
</socials>
```

Otherwise, the URL will be relative to your presskit, and thus, will break.

### Company `data.xml`

Your main `data.xml` containing your company information should use a `<company></company>` root tag for your XML document.

Before:

```xml
<?xml version="1.0" encoding="utf-8"?>
<game>
  <title>Pixelnest Studio</title>
  <!-- The rest -->
</game>
```

After:

```xml
<?xml version="1.0" encoding="utf-8"?>
<company>
  <title>Pixelnest Studio</title>
  <!-- The rest -->
</company>
```

**Why?** It allows us to better differentiate the main `data.xml` from the others. And moreover, it does not make sense that the company `data.xml` is considered as a `<game>`, right?

### Release dates

The original [presskit()][dopresskit] assumed that you had only one release date for a product or game. And we all know that it's simply not true.

That's why we handle multiple release dates.

So, in your product/game `data.xml`, you must change your `<release-date>` tag.

Before:

```xml
<?xml version="1.0" encoding="utf-8"?>
<product>
  <title>My Super Game</title>
  <release-date>04 Feb, 2016</release-date>
  <!-- The rest -->
</product>
```

After:

```xml
<?xml version="1.0" encoding="utf-8"?>
<product>
  <title>My Super Game</title>
  <release-dates>
    <release-date>PC/Mac - 04 Feb, 2016</release-date>
    <release-date>iOS/Android - 04 Feb, 2017</release-date>
  </release-dates>
  <!-- The rest -->
</product>
```

**Why?** We all know that there's no single release date for a product or a game.

---

## Credits

### [presskit()][dopresskit]

This couldn't have be made without the awesome work from the original [presskit()][dopresskit] team. Thanks to them!

### Assets

The images used in this repository can be found on [Unsplash](https://unsplash.com/), a free provider of high-quality images.


[dopresskit]: http://dopresskit.com
