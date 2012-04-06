---
layout: post
title: "Easy Rails debugging in IE with a Mac and VirtualBox"
date: 2011-12-13 11:37
comments: true
categories: ruby rails IE debugging
---
Internet Explorer is still more than 60% of my traffic, and I need to do a lot of feature testing on it. A lot of folks push up to a staging server then point a virtual machine to that server. This is too slow for me. Especially when I'm hunting down and fixing particularly pernicious css bugs, there is a lot of tweaking involved, and re-deploying for each test just doesn't cut it.

<!-- more -->

Instead, I setup VirtualBox to connect to my development server so I don't need to re-deploy to see changes in IE. It makes debugging in IE almost as easy as in other browsers!

Assuming you have, or can, setup VirtualBox with XP or Windows 7 (if not there are a thousand tutorials on google), the rest takes a couple of seconds. VirtualBox's default setting will allow it to connect to your Mac's localhost through `http://10.0.2.2`. Forwarding ports is messier, so instead we can run rails on port 80. This requires running your server as a super user. Assuming you're using rvm, run:

    rvmsudo rails server -p 80
    
and verify you can hit the server at `http://localhost` on your Mac, and `http://10.0.2.2` in VirtualBox. You're good to go!

While you're at it, I'd recommend installing [IE Collection](http://utilu.com/IECollection/), so that you can easily test on all versions of IE on the same box.
