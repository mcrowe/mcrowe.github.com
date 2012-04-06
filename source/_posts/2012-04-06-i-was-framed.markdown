---
layout: post
title: "I was framed!"
date: 2011-11-06 11:56
comments: true
categories: javascript
---
Patrolling the SERPs for a website I was working on one day, I came across something odd: An exact duplicate of my site at a different domain, startlingly high in the rankings. Here is its source:
<script src="https://gist.github.com/1439471.js?file=iframe_wrapper.html"></script>

<!-- more -->

OK, it's my site in an frame, fine. The comment, though, left me biting my nails. _Who are You_&mdash;capital _y_, no question-mark. Is it just me, or does that sound menacing? Was this meant for me? A way of getting my attention, the scraper knowing I would read the source of the site that hot-linked me? I was perturbed at having no clue what someone's motivation was for this. There was no way to profit that I could tell: users were still on _my_ site, just with a different domain. And, the hot-linking site used a real, 8-letter domain; too expensive to be a random attack. This was deliberate.

My first line of attack, of course, was to try to contact the offender and ask&mdash;kindly&mdash;that they stop ripping my site off. No luck. The domain was registered privately, and the previous owner couldn't help track down the buyer.

I quickly learned first-hand that this is an effective way to hurt the google rankings of a site, by pushing duplicate content up at a different domain. I can only assume that this was a trick played by one of my competitors to stop my site from getting traction, together with a menacing message to make me feel welcome. I'll be honest, I was/am definitely a little spooked. There are plenty of shady characters in my industry, and new competition is never greeted with open arms. Was I going to wake up to a couple of thugs banging my door down? OK, maybe I've watched too many thrillers, but you never know!

Once I got over being cheesed and worried, beating this attack was pretty easy. Adding a canonical url helps google and others learn (slowly) that yours is the real site, and this fixed our rankings. You can do this in Rails with Haml by adding:
<script src="https://gist.github.com/1439471.js?file=application.html.haml%20"></script>
to your `application.html.haml`.

I also added a frame-busting script which redirects the user to my site if they are viewing it in a frame or an iframe:
<script src="https://gist.github.com/1439471.js?file=frame_buster.js.coffee"></script>

This doesn't help with spiders or indexing as it relies on Javascript, but it does make sure that most users don't get trapped on the false domain. I got this idea from Jeff Atwood's [article on frame busting](http://www.codinghorror.com/blog/2009/06/we-done-been-framed.html). As Jeff points out, the wrapping page has the last say on Javascript, so it can always beat any tricks like this, but you can at least make it frustrating for them to try! (Note that this technique will interfere with some tools you might use which show your site in an iframe, such as google analytics' in-page analytics. You could add a whitelist feature to this, but I didn't need to.)

No bats to my knees so far. Knock on wood...
