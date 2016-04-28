---
layout: post
title: Starting off my fantasy football web application
tags: django, mysql, fantasy football
---
One of my favorite things in life is football. Mainly, it's my love for my Michigan Wolverines (go blue!) but my love for fantasy football comes in at a close second.

That being said, I haven't won my fantasy league yet. Three years of making the playoffs, but never getting to the championship game. Sigh. But that's the great thing about fantasy football; no matter how close I come (and ultimately fail to win) to the championship, I still love it to death.

So, that being said, I've been dying to combine my love of fantasy football with my love of programming. For the past two years, I've been toying with the idea of creating some form of app related to it, but I've never had a great idea nor a good method/thought/idea for implementing it. This year, however, I think I have a good idea to help me learn more programming skills, as well as help me in the my fantasy league (hopefully)... and maybe (waaaay down the line, of course), it'll be a tool I could provide to the masses. But, I think the first step is creating this application.

To start of, my preliminary idea for this application is a web based (what I'm going to call a) "portal". My thought would be that this portal is essentially just a dashboard that you can use to pull up a player(s)/team(s) basic information; essentially, something that you would see in ESPN's "clubhouse" view, but with more fantasy-centric information. The best part about this is that I already have a data set for this (shout out to armchair analysis).  [Armchair Analysis](http://www.armchairanalysis.com/) does a great job of providing detailed and affordable football statistics, which (for cheap) you can download after the season ends.

My thoughts to implement this would to be to use:

  - Django as my backend/web-server

  - MySQL as my DBMS, within django

  - ReactJS as my front-end UI management

  - Have D3.js integration within my front-end UI
  
This is... a lot, for me. I'm definitely pretty comfortable with Django now, but I just started learning ReactJS and I've never used MySQL before[^1].

That being said, I'm super excited to learn. I can't wait to get into this, and I'll definitely be posting blog entries on here as I go. Hopefully, this will aid in my programming knowledge and, maybe, someone might find my struggles entertaining or enlightening (aka please learn from all the stupid mistakes I make).

Anyways, enough out of me. Thanks for reading, and have a good one!



[^1]: Oh my god was tonight was frustrating. I had a pretty difficult time getting MySQL set up on my computer. For a while (after the installation), I didn't realize I was assigned a temporary password to set up my root user (which meant A. I couldn't set up my root user password and B. I couldn't even use Mysql...). But then I did a bunch of google searches for ways to set up my root password (I couldn't even open the damn MySQL shell), all of which failed. For one reason or another. I finally realized that Mysql has documentation that details how to reset the root password, and that worked like a charm. So, lesson learned - go straight to the source to figure out how to solve an issue.
