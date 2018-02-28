---
published: false
layout: post
title:  Accessibility testing, with 'pa11y-ci'
date:   2018-02-28 21:35
tags:   [ a11y, travis-ci, "open source", nodejs, javascript ]
og-desc: A short description
og-image: https://..
og-image-alt: ALT text.

last_updated: 2018-02-28
changefreq: daily
priority: 1.0
---

I've recently come across [pa11y-ci][], and I'm impressed with how easy
it is to use for automated accessibility testing.

`pa11y-ci` is written in Javascript for Node.js.
It is built on top of [pa11y][], and [HTML_CodeSniffer][].
And, it integrates well with [continuous integration][ci] platforms like [Travis-CI][].

To get started, run this command in your terminal:

```sh
npm install pa11y-ci --save-dev
```

Create a configuration file named [`.pa11yci.json`][.pa11y], specifying
a `standard`, some `urls` and other options. Here's an example:

```json
{
  "#": "Automated accessibility testing ~ https://github.com/pa11y/pa11y-ci",

  "defaults": {
    "standard": "WCAG2AAA",
    "timeout": 5000,
    "wait": 2000,
    "verifyPage": "gaad-widget-js"
  },
  "urls": [
    "http://127.0.0.1:9001/embed/?gaadwidget=force&...",
    "http://127.0.0.1:9001/test/static.html?..."
  ]
}
```

I'm eschewing [Grunt][] et al, and simply adding `scripts` to my `package.json`:

```json
{
  "devDependencies": {
    "pa11y-ci": "^1.3.1"
  },
  "scripts": {
    "pa11y-ci": "pa11y-ci --config .pa11yci.json"
  }
}
```

Here's a more complete [`package.json`][pkg]:

```json
{
  "name": "gaad-widget",

  "devDependencies": {
    "live-server": "^1.2.0",

    "pa11y-ci": "^1.3.1"
  },
  "scripts": {
    "test": "npm run pa11y-ci && echo other commands ..",
    "serve-ci": "live-server --port=9001 -V --no-browser --watch=DUMMY",

    "pa11y": "pa11y --standard WCAG2AAA http://127.0.0.1:9001/#..",
    "pa11y-ci": "pa11y-ci --config .pa11yci.json"
  }
}
```

And, here is a simplified [`.travis.yml`][trav]:

```yaml
language: node_js

node_js: 8

git:
  depth: 8

install: npm install

before_script: npm run build

script:
  - npm test
  - npm run serve-ci & sleep 5; npm run pa11y-ci;
```

The above results in this [Travis-CI job output][job]:

```
> pa11y-ci --config .pa11yci.json
Running Pa11y on 2 URLs:
GET /embed/?gaadwidget=force&_ua=pa11y-ci 200 28.105 ms - 1708
GET /test/static.html?_ua=pa11y-ci 200 30.170 ms - 1792
GET /dist/gaad-widget.js 200 4.013 ms - 12631
GET /style/gaad-widget.css 200 3.276 ms - 1125
 > http://127.0.0.1:9001/embed/?gaadwidget=force&_ua=pa11y-ci - 0 errors
 > http://127.0.0.1:9001/test/static.html?_ua=pa11y-ci - 0 errors
✔ 2/2 URLs passed
```

The good:

 * The [Cloudworks][] home-page
 * [gaad-widget][]

The bad:

 * [The comments on my blog][blog] :(
 * ...

If you'd like to use `pa11y-ci`, why not add a badge to your README?

[![Accessibility testing - GAAD passes][pa11y-icon]][pa11y-ci]


---

[!['Kitten' photograph][kitten-img]][kitten]

[kitten-img]: https://c1.staticflickr.com/6/5027/5558881213_deb384bdb8_z.jpg
[kitten]: https://flickr.com/photos/barbarellathemadcatlady/5558881213
    "Kitten, by Barbarella Buchner, 25 March 2011. License: CC-BY-SA-2.0"

[pa11y]: http://pa11y.org/
[gh-pa11y]: https://github.com/pa11y/pa11y
[pa11y-ci]: https://github.com/pa11y/pa11y-ci
[travis-ci]: https://travis-ci.org/nfreear/gaad-widget
[job]: https://travis-ci.org/nfreear/gaad-widget/jobs/347455031#L1083-L1104
[pa11y-icon]: https://img.shields.io/badge/accessibility-pa11y--ci-blue.svg
[HTML_CodeSniffer]: http://squizlabs.github.io/HTML_CodeSniffer/
[ci]: https://en.wikipedia.org/wiki/Continuous_integration
[grunt]: https://gruntjs.com/

[pkg]: https://github.com/nfreear/gaad-widget/blob/3.x/package.json#L1 "package.json"
[trav]: https://github.com/nfreear/gaad-widget/blob/3.x/.travis.yml#L1 ".travis.yml"
[.pa11y]: https://github.com/nfreear/gaad-widget/blob/3.x/.pa11yci.json#L1 ".pa11yci.json"

[gaad-widget]: https://github.com/nfreear/gaad-widget
[cloudworks]: http://cloudworks.ac.uk/
[blog]: #

[End]: //.
