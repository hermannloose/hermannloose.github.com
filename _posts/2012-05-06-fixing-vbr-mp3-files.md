---
layout: post
title: How to fix VBR MP3s with borken track length
meta:
  description: A short blog post about a tool for fixing VBR MP3 track lengths on Ubuntu.
tags:
  - english
lastmod: 2012-08-24T23:00:00+02:00
---

I just came across [vbrfix](http://home.gna.org/vbrfix/), a very handy tool to
fix MP3 track lengths that seem to be off, which according to [the
manpage](http://manpages.ubuntu.com/manpages/precise/man1/vbrfix.1.html) can be
caused by bad VBR encoders. Like ancient versions of Windows Media Player, as
I only ever had this problem with one album and I probably ripped that when
I was twelve. (Just kidding, I didn't even have my own CD player back then,
much less MP3.)

Usage is a no-brainer, messed up MP3 goes in, shiny new MP3 with correct track
length pops out. What I didn't try yet is in-place corrections, but that
probably works fine as well.

*Why would you want to do this, other than OCD?*

Well, it appears to throw off Last.fm scrobblers quite a bit. Say Banshee sees
a track that's 25 minutes long and finishes playing after three minutes: "less
than 50% played" = no scrobble. I know. This results in precious track plays
being lost for [bands that deserve a lot more
exposure](http://www.last.fm/music/A+Subtle+Plague).

*Which is still OCD, now that I think about it.*
