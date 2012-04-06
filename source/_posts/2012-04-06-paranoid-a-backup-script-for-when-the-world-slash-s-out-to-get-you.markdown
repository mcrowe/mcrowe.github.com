---
layout: post
title: "Paranoid - A backup script for when the world\'s out to get you"
date: 2011-11-07 16:28
comments: true
categories: ruby thor
---
When I've put a ton of effort into a personal project, I tend to get paranoid that I'll somehow find a way to toast it. I know, I know, git, github, and time machine already have my back. Sometimes that's just not enough, though, and I find myself periodically making manual copies of important projects to a backup directory. Whether I need it or not, having hardcopy snapshots just makes me feel better.

<!-- more -->

So I wrote paranoid, a Thor script for those paranoid but lazy coders like me. Sure, we could use a one-liner `cp -rf`, or `rsync` command, but there are a few niceties that paranoid gives you:

* Timestamped backups, so they are never written over, and you can easily revisit a snapshot of the project at any given time. 

* You can specify files to exclude from a backup on a project-by-project basis by modifying a `.backupignore` file. This allows you to ignore `.git` and `.bundle` directories as well as any project specific files such as large data dumps that you might not want copied over and over. 

### Install paranoid
Paranoid is a [Thor](https://github.com/wycats/thor) script, and you will have to install Thor first. Then, clone the repository and run: `thor install paranoid.thor`

### Make your projects paranoid
In your project root directory, run: `thor paranoid init`
This creates a default `.backupignore` file. This file defines patterns for files you don't want to backup in this project. You can now add or remove patterns as you wish.

### Backup a paranoid project
In your project root directory, run: `thor paranoid backup`
This rsyncs your project to the `~/.paranoid` directory, ignoring any files matching the patterns in the project's `.backupignore` file.