---
layout: post
title: "Soulmate.js—A jQuery front-end to the soulmate auto-suggestion gem"
date: 2011-12-20 12:51
comments: true
categories: javascript coffeescript jQuery
---
[Soulmate](https://github.com/seatgeek/soulmate) is an excellent auto-suggestion gem built for speed on sinatra and redis. I recently switched a project's auto-suggestion engine to it from sphinx, and saw 200ms average response times drop to 10ms. Aside from speed, another huge boon was being able to completely separate the auto-suggestion engine from the main app. This allows it to get overwhelmed with a huge number of requests without significantly affecting the user's experience. (Decoupling is good!).

<!-- more -->

Soulmate provides a very nice http interface and leaves the front-end design up to the developer. I wrote [soulmate.js](https://github.com/mcrowe/soulmate.js), a jQuery front-end to soulmate. Together, they provide lightning-fast plug-n-play auto-suggestion. Soulmate.js boasts the following features:

* **Well tested:** Ridiculous spec coverage using Jasmine.
* **Clean markup:** Renders a clean and semantic markup structure that is easy to style.
* **Speed:** Minimizes requests by maintaining a list of queries with no suggestions. No additional requests are made when a user keeps typing on an empty query.
* **Cross-domain compatible:** Uses jsonp to accommodate backends on separate domain (which is a good practice since it allows the auto-suggest system to get overwhelmed without affecting the main site).
* **Customizable behaviour:** Customized rendering of suggestions through a callback that provides all stored data for that suggestion. Customized suggestion selection behaviour through a callback.
* **Adaptable:** A modular, object-oriented design, that is meant to be very easy to adapt and modify.

For more information, check out the README and specs on [github](https://github.com/mcrowe/soulmate.js).
