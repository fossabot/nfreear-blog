---
layout: post
title:  ISAD-widget
date:   2017-09-04 18:00
tags:   [ NPM, accessibility, "open source", event, javascript, stammer ]
og-desc: To help promote and celebrate International Stuttering Awareness Day (ISAD), I’ve come up with an Javascripted banner-link.
# og-image-00: https://c1.staticflickr.com/5/4076/35671915106_62be509598_z.jpg
og-image: https://unpkg.com/isad-widget@1.0.1-beta/style/isad-widget.jpg
og-image-alt: ISAD-widget embedded on a web-page.
---


Sunday 22nd October 2017 will be the twentieth [International Stuttering Awareness Day (ISAD)][isad],
an initiative jointly founded by the European League of Stuttering Associations,
the International Fluency Association, and the International Stuttering Association.

ISAD serves an important purpose in explaining the speech disorder,
also called stammering, which affects 1% of the population across the world,
and which is still often mis-understood.

After my recent work on a [GAAD-widget][], I thought I'd do my bit by creating
a banner link that can be added easily to a web site, and that appears for
a pre-determined period before and after the day (_22nd October each year_).

See the code on [NPMJS][] and [GitHub][].
It can be embedded on a page with the following _two lines_ of HTML
— it requires zero configuration by default:

```html
<div id="isad-widget"></div>

<script src="https://unpkg.com/isad-widget@1.0.1-beta#._.js"></script>
```

(_Thanks [unpkg][]!_)

(_Note, you need permission to add the Javascript to your website, as shown above.
Not all users who are "authors" will have that permission._)

This version is very basic. I thought I'd get it out, and gauge the response.

I'd love to hear whether you think it's useful, and what features you'd like.
(_[Force display][force]._)

Some ideas I've had:

* Better visual design (_I'm not a designer!_)
* Methods for easier installation, for example, a WordPress plugin,
* Configurable number of days before and after,
* Support for multiple languages,
* Add publicity for the [ISAD conference][isad-conf] (e.g. "_Conference day 2_")
* _... ?_

Note, the code is released under the open-source [MIT license][mit].

Please feedback via the [comments](#comments), to [@nfreear on Twitter][], and [on Facebook][].

[![The widget - link to ISAD][widget-img]][isad]


[@nfreear on Twitter]: https://twitter.com/nfreear
[on Facebook]: https://facebook.com/nickfreear
[force]: ?isad-widget=force

[isad]: http://isastutter.org/what-we-do/isad?utm_source=github&utm_campaign=isad-widget
[isad-conf]: http://isad.isastutter.org/isad/
[wiki-isad]: https://en.wikipedia.org/wiki/International_Stuttering_Awareness_Day
[gaad-widget]: /2017/05/14/gaad-widget.html "Global accessibility awareness day ~ 'gaad-widget'"
[npmjs]: https://npmjs.com/package/isad-widget
[github]: https://github.com/nfreear/isad-widget
[unpkg]: https://unpkg.com "unpkg is a fast content delivery network for everything on npm."
[mit]: https://nfreear.mit-license.org/2017#!-isad-widget "MIT License (code)"
[widget-img]: https://raw.githubusercontent.com/nfreear/isad-widget/1.0.1-beta/style/isad-widget.jpg
[widget-img-00]: https://unpkg.com/isad-widget@1.0.1-beta/style/isad-widget.jpg

[End]: //.
