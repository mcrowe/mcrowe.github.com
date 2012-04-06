---
layout: post
title: "Filtering Pop-ups From Embedded Scripts"
date: 2011-11-07 12:05
comments: true
categories: javascript
---
Recently I had a problem where a creative embedded on my site was periodically opening pop-ups on my users without my consent. The agency's team assured me this shouldn't be happening, but claimed they couldn't re-create the issue. In truth, they just sell too many third-party ads to verify all of them.

<!-- more -->

Since these ads are breaking their agreement, I felt it was in my right to block them for my users. I decided to create a filter in my pages to block embedded scripts from opening unwanted windows. I couldn't find anything good about this on the internets, so I thought I'd share the solution I came up with.

My first stab at the problem was to override the `window.open` function (which the offending script would be calling). I made it silently do nothing when called, by redefining it as a stub:
<script src="https://gist.github.com/1440000.js?file=popup_blocker.js.coffee"></script>

These few characters did the trick. Any code trying to open a pop-up fires the new `window.open` and happily continues on its way, unaware that no window was actually open.

I was happy with this solution until, one day, I tried including [addthis](http://www.addthis.com) on the site. The addthis widget opens a pop-up for many of its providers, and my hack, of course, dutifully blocks it every time! Alas, it seems a site sometimes needs to be able to open pop-ups for the powers of good... 

We need to be able to filter requested pop-ups: allowing the ones we trust, and blocking the rest. So, I created a whitelist filter on `window.open` by first saving an aliased copy, and then redefining it to a new method that conditionally calls the copy. 
<script src="https://gist.github.com/1440000.js?file=popup_filter.js.coffee"></script>

Now, when `window.open('http://www.addthis.com/...', ...)` gets called, the regular expression matches and the aliased method gets called just as the addthis widget expects. However, when `window.open('http://nefarious-ad-site/...', ...)` gets called, the request is nicely eaten up. 

Cool! We can now manually filter pop-ups from opening on our site based on the requested url.

**Footnotes**

* These code samples are coffeescript, of course, not javascript. I'm sure you can use your creativity to compile them in your head if you need to.

* Both these techniques were tested and work in IE8+, Firefox 3.6+, Chrome, and Safari. Other browsers, no idea.

* This technique will not work out of the box to filter pop-ups opened from scripts loaded within iframes. You may be able to modify this to handle that case.
