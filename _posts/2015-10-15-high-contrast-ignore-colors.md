---
layout: post
title:  High contrast and ignore colours
x-created:  2015-10-15 22:00:00
date:   2015-10-23 15:20:00 +0000
categories:
tags:   ignore-color  accessibility  low-vision  fixes  javascript  css
---



Recently, I've been doing some accessibility fixes for a project I maintain
-- the [LACE Evidence Hub][] ([I talked about it][talk]).
I am also doing some accessibility evaluations of other sites.

And so, I've been revisiting some work I did previously for [Open Media Player][] on fixing high-contrast related bugs and issues

<!--more-->

Before we get into the meat of the post, I'll recap why high contrast and ignore colour settings matter.
People with low vision use a [number of techniques to read text and web sites][webaim].
They may use a screen magnifier, or zoom in with their browser. And, those users who struggle to perceive contrast, may employ the high contrast settings built into operating systems including Windows.
Or, they may set their browsers to ignore the colours and styles specified by a web site.


Under such settings, background images used on buttons and elsewhere will disappear, and subtle borders which help to demarcate regions of a page can become invisible. Suddenly, an apparently beautiful page becomes much harder to comprehend!

Obviously, it's better to consider this situation upfront, and take care how background images and other styling is used. However, if you find that you need to fix a site after the fact, is there anything you can do?

Yes!

This accessibility fix comprises two parts.

This is one of the rare cases where we can detect how the user has set up their computer. First, the small Javascript script, [ignore-color.jquery.js][js], can be employed. It runs a test periodically by creating a hidden HTML element, setting its background colour, then detecting if the specified colour is still in use. If the user has used any sort of high contrast or "ignore-colour" setting in the operating system or browser, then the assigned colour will not be used -- the test will "fail".

The Javascript uses the result of the test to set a class on the `<body>` of the web page --
either `ignore-color` or `no-ignore-color`. The Javascript is fairly lightweight --
the only cost is that the test is run [every 4-8 seconds][tag-int] via `setInterval()`.
(As far as I know, there is no alternative -- ideally one would detect a Javascript event fired when the user changes their configuration.)

Note, the `ignore-color` Javascript is based on [work by John Snyders][work].

While the first part of the fix is fairly generic, the second part is specific to each web site.
The body-class set by the Javascript can be employed in CSS stylesheets, to take remedial actions.

A lot of the CSS fixes will involve colours and colour combinations. Your initial reaction
may be -- help! "I don't know what specific settings or high-contrast theme the user has
chosen. So, how do I select safe colours?"

The answer can be found in the use of [operating system styles][sitepoint].
These are a set of pre-defined terms in CSS, that tell the browser to use your
computer's operating system colours -- whatever they may be.


An example follows from the [LACE project][css] --
note this is applied to SVG, hence the use of `stroke`:

{% highlight css %}
.ignore-color svg #sandisplay .link {
        stroke: Highlight;
}
{% endhighlight %}

`Highlight` is one of the pre-defined system styles, which produces the green
Sankey diagram on the right of the first screen shot.

[![Screen shot 1 - high contrast Sankey SVG][img-1]][slideshare]


The next CSS example is applied to form fields, and uses the pre-defined term `ButtonText`.
Note, the `border-style` property must be `inset` to overcome a Firefox restriction or bug.

{% highlight css %}
/* Firefox requires "inset" in ignore-color mode for form fields. */
.ignore-color input, .ignore-color textarea {
        border: 2px inset ButtonText;
        box-shadow: none;
}
{% endhighlight %}

And, here's a screen shot showing the result of the fix, on the right.

![Screen shot 2 - ignore-colour form & video][img-2]


So there you have it.
[Re-usable Javascript][js], and an example of [CSS stylesheet fixes][css].

Now. Go experiment.



[LACE Evidence Hub]: http://evidence.laceproject.eu
[talk]: /2015/10/09/laceflare-workshop-lace-accessibility.html
[slideshare]: http://slideshare.net/laceproject/learning-analytics-lace-solar-flare-2015/11
[Open Media Player]: http://iet-ou.github.io/open-media-player
[webaim]: http://webaim.org/articles/visual/lowvision "WebAIM - Web accessibility in mind"
[useful]: http://ux.stackexchange.com/questions/27992/is-high-contrast-mode-really-useful

[js]: https://gist.github.com/nfreear/c82581b4485cd303150d "ignore-color.jquery.js – License: MIT. On GitHub"
[work]: http://hardlikesoftware.com/weblog/2009/11/04/css-sprites-vs-high-contrast-mode/
    "CSS sprites vs. high contrast mode, November 4, 2009, by John Snyders (public domain)"

[css]: https://github.com/IET-OU/wp-iet-generic-plugins/blob/master/css/wp-eh-ignore-color.css#L19-L22
    "wp-eh-ignore-color.css – on GitHub"
[sys]: http://webdesign.about.com/od/colorcharts/l/blsystemcolors.htm
[sitepoint]: http://www.sitepoint.com/css-system-styles/
    "How to Use Operating System Styles in CSS, by Craig Buckler, August 11, 2009"
[satis]: http://iet-embed-acct.open.ac.uk/satis/#!/ignore

[slide]: https://docs.google.com/presentation/d/1xkJz6FO6sC07ED7s6fsy4ZR3ds4zDl1jTdsFfEge4Ns/edit#
[img-1]: https://lh3.googleusercontent.com/_9KTY0jDnn8XoToAQc1zDxgOteSlgH_sEEyq7A79hcD6WDq4HjWJXO-NK5xYi40UzXWRY_QxAuhcXpQfBgOspZbzQicTvzT2p_QdDMlVMHN2mubr6VI-PuVOhApvM4YUvd_rf8Nv1A
    "Screen shot 1 – before and after the fix"
[img-2]: https://lh3.googleusercontent.com/-Na-bOj5r05cha_DyhpejXsEz9fuQ8nUXznee_Y3lSKkUCp1IYECt4iCFkvs4Yn4j3ksYW7SuTvsh8iv8V6l2ZsyGTC3JyhbUadz9mZxLTDIDKv-1SqUkC-MNNcEpKcVm1wzBPDNow
    "Screen shot 2 – before and after the fix"

[tag-X]: javascript:return%20false "You decide!"
[tag-int]: #!tag "You decide the time interval! We try to strike a balance.."

[End]: end
