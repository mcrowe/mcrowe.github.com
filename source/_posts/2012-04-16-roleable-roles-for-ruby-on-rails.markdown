---
layout: post
title: "Roleable roles for Ruby on Rails"
date: 2012-04-16 20:45
comments: true
categories: ruby, rails
---

I was searching for just the right roles system to go with my `cancan` authorized, `ActiveRecord`-backed Rails app, and didn't find anything I liked. There are at least a dozen gems out there, but they were all either too simple, too complex, or too ugly for my liking. So, like any good open-sourcer, I wrote my own after my biased taste. And, `roleable` was born. Check out the [project page](https://github.com/mcrowe/roleable), and the [API documentation](http://rubydoc.info/gems/roleable/frames). 

`roleable` is deliberately simple in it's implementation. It allows you to add user roles scoped to a instance of another model (e.g. make a use an author of a given article), or global roles (e.g. an admin role).
