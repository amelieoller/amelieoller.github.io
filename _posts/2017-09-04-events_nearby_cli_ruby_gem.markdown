---
layout: post
title:  "'Events Nearby' CLI Ruby Gem"
date:   2017-09-04 18:41:58 +0000
---


Developing my first Ruby Gem was quite an experience. There were ups and downs just like with almost any programming project – but that’s what I love about programming. Also, trying to consistently commit your changes with git took some getting used to.

It took a few days, but I finally published my first gem – it’s called *Events Nearby*, and lets you enter any location to retrieve a list of events that are near that location. It shows you a numbered list of nearby events, when they are taking place, where they are exactly, and how much they cost. You can then choose one of the listed events, get more information on it, and even open the event page in your browser. The gem works by scraping the eventbrite.com results list for the specified location.

I doubt anyone is going to use it, because, let's face it, who looks for events nearby through their commandline? It's probably easier just to head over to eventbrite.com. But that's fine. I built this gem to gain knowlege and to learn more about programming a gem - now I'm confident I can repeat the process, maybe with a more useful gem next time.

There are definitely improvements still to be done, but for now it works as it should. Some additional functionality could include:
* Sorting the event results by price or by date
* Retrieving event results based on a specified price or date
* Returning a useful error message for an incorrect city entry
