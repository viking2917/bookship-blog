---
layout: single
title:  "Anatomy of a Hack - Books, Music & CODEX"
date: "2016-01-13"
categories: 
  - "publishing"
tags: 
  - "books"
  - "hackathons"
  - "music"
coverImage: "e5a6c-1zh_jyon3zobk5x228tb4cq.jpeg"
---

![]({{ site.url }}{{ site.baseurl }}/assets/images/e5a6c-1zh_jyon3zobk5x228tb4cq.jpeg)

Awhile back I randomly found out about [CODEX Hackathon,](http://codexhackathon.com) a “literary hackathon” mashing up books and technology, and I knew I had to get involved. I started by registering to attend, but realized pretty quickly I wanted to do more. I volunteered to helped organize and sponsor, which I’ll write about later. I also hacked, and wanted to share what I came up with, and how I came up with it.

https://open.spotify.com/user/viking2917/playlist/7jZS1eOs4879cWN4dPqJgs

I’ve been interested in the intersection of books and music for awhile. I used to write [book reviews with embedded playlists](http://www.viking2917.com/tijuana-straights-by-kem-nunn/) of what I was listening to while I read the book. Or make playlists of music mentioned in a particular book - for example, the [early jazz mentioned](https://open.spotify.com/user/viking2917/playlist/7jZS1eOs4879cWN4dPqJgs) in Kathleen Ann Goonan’s In War Times. Or read [interviews where authors talk about the music that inspired them](http://www.largeheartedboy.com/blog/archive/2007/04/book_notes_eliz.html) as they wrote.

And write why Books & Music go together like Wine & Chocolate.

{% include card.html link="https://medium.com/p/4203589ebb6b" %}

So when this hackathon came along, the juices had been flowing for awhile and I knew what I wanted to do. Build an environment where people could collaboratively build and share music playlists for their favorite books.

I had the basic idea framed out in my head. I’d use the Spotify web player and hack up a branch of [http://www.thehawaiiproject.com](http://www.thehawaiiproject.com) to become the new thing. Seemed like a layup, all their Web APIs are sitting right there. Spotify has a feature for “collaborative playlists” - what could go wrong, right?

After some presentations from sponsors (I was a sponsor, here was my pitch for [The Hawaii Project](http://www.slideshare.net/viking2917/the-hawaii-project-codex-2016-hackathon)), we get down to it, at 11am Saturday morning.

Here’s a quick timeline from my notes:

> start @ 11  
> around 12, have a Master & Commander (Patrick O'Brien’s book) page with a static playlist on it. Everything hard coded but I can listen to music for the book and it visually looks pretty good!

My plan is to use Spotify’s Collaborative Playlist feature so everyone can add to the playlist (and be authenticated to Spotify in the normal way via their browser). **SNAG**! Turns out making a Playlist “Collaborative” in Spotify makes it Private so only collaborators can see it. Even worse, via the API, only the Owner can modify it. That pretty much blows the whole idea out of the water.

OK, Plan B. I will make a Hawaii Project Spotify account that will own all the playlists. When users add an item to a playlist I’ll send it to my server and the server will add it to the playlist. Because the API calls have to authenticate (via OAuth) to the Spotify server, I have to figure out how to authenticate in PHP to Spotify without a browser around. I dumpster dive in Stackover flow and find [The Hint](http://stackoverflow.com/questions/31281390/spotify-api-authorization-for-cron-job) (thank you [Michael Thelin](https://medium.com/u/3d7800b699b4)!).

> 12:00 : 1:30pm. I struggle to get The Hint to work in practice. I take a break and grab lunch (wonderful sandwiches and Hummus, CODEX has great food!).  
> 3:41pm EUREKA!!!! I get a valid spotify token and successfully retrieve a playlist!!!!!  
> 3:42pm. My token expires and I can’t figure out how to get it to renew.  
> 7:45pm. I think I get a repeatable way to add tracks, at least until my token expires. which I have to renew manually. OK for a demo but can’t actually go live with that. I’ve spent ~50% of my hacking time on OAuth. Not what I had in mind.  
> 8:30pm. I have some basic track search + autosuggest for tracks working. (like when you type “Stairway to H” I suggest “Stairway to Heaven by Led Zeppelin”)  
> 8:50 Stairway to Heaven and Highway to Hell added to playlist via UI. !!!!!!  
> 9:50 Code cleanup. Things basically working with a single hard-coded book & playlist ID, except hacky tokens & expiration.  
> 10:00 Did I mention this is a hackathon for Adults? MIT kicks us out at 10pm. Home. Martini. Sleep.

> Sunday  
> 6:30 am up, by 7:40am On the train.  
> 8–9 in coffee shop because MIT doors locked. Quickly solve some problems with playlist views and track list ordering problems solved. still struggling with expiring oauth tokens.  
> 10:00 With the exception of tokens, I have what I need for a workable demo, can search for and add tracks to any book.  
> 10:30–11. Make some fun playlists for some of my favorite books!  
> 11:12 roll a new home page showing the latest books that have soundtracks created.  
> 12:30. stop and roll a deck for the presentation.  
> 1pm. Hands off the keyboard at 2pm for presentations, so I decided to adopt the “Vietnam strategy”. Declare victory and get out. I avoid breaking my demo with any late changes, and go chat with a few interesting folks I didn’t have time to get to before.

Presentation went well (in fact everyone’s did!). I start my presentation with the James Bond theme and end with adding Highway to Hell to a playlist, and playing it over the speakers as I exit. **Mission Accomplished**.

I wanted to launch it to a live URL during the Hackathon, but I just couldn’t solve the expiring token. On the drive home, I decided that tomorrow I’d ask my son-in-law, who is an actual practicing software engineer. But I wake up the next morning and, as often happens, within about 20 seconds I see a typo that’s been causing me all this grief. Edit, “git commit -m “I’m an idiot””, and a few minutes later, voilá: [BookPlaylist](http://www.bookplaylist.com) is born!

As I write this, I’m jamming to Kayti’s most excellent playlist to Cinder, a book I’ve not read. But now might.

{% include card.html link="https://medium.com/p/4203589ebb6b" %}

It was really fun to take an idea that I’ve had in my head for almost a year, and get it out of my head and into something real. Hope you get a chance to play (pun intended) with it!

You can read a bit more about the Hackathon here (via [Matthew S Carroll,](https://medium.com/u/14490ba48eea) one of the organizers.

{% include card.html link="https://medium.com/p/4203589ebb6b" %}

Xconomy has a great writeup here: [xconomy.com/boston/2016/01/12/glimpsing-digital-publishings-future-at-codex-hackathon-at-mit/](http://xconomy.com/boston/2016/01/12/glimpsing-digital-publishings-future-at-codex-hackathon-at-mit/)

In later posts, I’ll write about the technical tools we made available for participants.
