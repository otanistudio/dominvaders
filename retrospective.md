# DOM Invaders! Retrospective

Here are some notes to share my learnings. If anything, this retrospective is just an exercise in providing closure to this micro-project.

## Goals

Main goal: __ship__ a [playable game][dominvaders] using very basic web technology while riding the train for an hour.

After playing with iOS and Objective-C for the past year, I wanted to do more things with JavaScript. Going to [GDC2012](http://www.gdconf.com/ "Game Developer's Conference 2012") inspired me to write a game while taking a train ride.

To add a bit of excitement, I announced _via_ [tweet](https://twitter.com/#!/otanistudio/status/178149805032345600) that I'd do this. Knowing that I could be ridiculed is an interesting motivator. The added stress of a train environment, with all its bumps, noises, intermittent WiFi, and passenger body odors added another layer of challenge.

Were my goals met? Yes, though I have to say I fell short of hitting it out of the ballpark: A solid double with a RBI. The shipped game can be played at [http://otanistudio.github.com/dominvaders/][dominvaders].

## Tech

I sought to use the smallest, simplest libraries available.

* [underscore.js][underscore]: For the array mappings and equality testing alone, you'll want 
  this, but oh! It's so much more than that.
* [qwery][qwery], a CSS 1, 2, or 3 selector engine that's both _tiny_ and _fast_.
* [bean](https://github.com/fat/bean "Bean JS"), Yet another _tiny_ and _fast_ library. This one
  deals with events.
* [bonzo](https://github.com/ded/bonzo "Bonzo JS")... ok these are all _tiny_ and _fast_. 
  This guy is a DOM utility. Not only do you get things like `hide()`, but paried with [qwery][qwery] above, now you can do this: `$('div#mydivid').hide()`

I "combined" these libraries using [Ender][ender], a _schweet_ little JS package management sytem. It is such a great tool because it lets me bring to the field only what I need. If all I want is a CSS selector engine with an event manager, I can build it. If I find out later that I didn't need a library, I can remove it. All of the (loosely-coupled) dependencies simply live in a single `ender.js` file.

Given the time and resource constraints, optimization wasn't on the top of the list. Rather, I stuck with some habitual "best practices," which turned out to produce fairly reliable code while minimizing the need to remember all the little details.

* Since we're limited to one thread, use a single timer (_ref._ `setInterval`)
* Animated GIFs are another thread, and I already made them a long time ago, so no need to worry about syncing spritesheet animations within the same timer
* Instead of namespacing a simple game, just protect the vars by wrapping code in `!function(){}()` (the more terse and [sometimes faster](http://jsperf.com/bang-function "!function performance tests") alternative to `(function(){})()`)

Another small speed edge gained via a few shortcuts:

* Didn't worry about semicolons. Some developers don't like this, but for the one-hour goal, it cleared away a bit of cognitive friction.
* Commas in front of variables in long `var` declarations means that I'm far less likely to miss delimiting those variables as I add, move, or delete them. (If you're OCD about performance, there's  a [teeny benefit](http://jsperf.com/vars-comma/2).)
* Text editor? I tried out [Sublime][sublime] _(Mac, Win, Linux)_, was very happy with it, and have been using it every day since. If you have a Mac and have been living under a rock, [TextMate](http://macromates.com/ "TextMate Text Editor for Mac") is also superb.

## The Good

* Got me in that "JavaScript Groove" I was looking for. I'm ready to write even more!
* _Focus._ Even though it took me a few train stops before I could really shut out the distractions, when the focus finally
  happened, I was in the immersive [flow state](http://bit.ly/4akhtJ 'Wikipedia on Flow State'). This left me in a
  [more positive psychological mood](http://instagr.am/p/H-TDs-hI_D/ 'Cured Pork Parts Also Make Me Happy') for the rest of the day.
* [_Mise en place:_](http://en.wikipedia.org/wiki/Mise_en_place "Everything in its place") Getting the basics in place helped a ton. Cooking shows and every decent restaurant does this. They have all their ingredients washed, chopped, peeled and measured. This lets one present a more focused path of how the ingredients are put together to form the _gestalt._
    * Had the graphics already rendered out and a plan for how to place them
    * Did some research on how [CSS keyframes](https://developer.mozilla.org/en/CSS/@keyframes) 
    worked. Without this, I would have spent too much time synchronizing explosion animations with the main game loop.
* Libraries: See the [Ender][ender] nod above. They were all I needed to get the job done quickly; everything will look familiar to [jQuery](http://jquery.com 'jQuery JS Library') developers.
* [Github][github]: using it was a pure joy. It was the "perfect" tool for showing my batched commits in near-real time, and [Github Pages](http://pages.github.com/ "Github Pages") was very convenient to use as a host for the [shipped product][dominvaders].

## The Bad

_This is where the actual good learnings come from!_

Estimates are always a hunch, but you still have to go for it. Empirically speaking, they are unreliable. The key is to not dwell on them for too long, and to err on the side of _going for it!_ (Once the work is underway, you'll know soon enough when you've taken on too much or too little.)

Even though I had a map in my head about how I was going to navigate the problem, I had never done anything like this on the train. Even though being in an immersive flow state was great, it took me longer than I had expected to actually get there. I thought it would cost a third of the ride, but it had actually cost close to half of the ride. That aspect of the experience was predictably unpredictable.

* Missed features
    * Scoring
    * UFO flying across the top at random intervals
    * Invaders firing back at _you_
    * Shrinking boundaries as the invader list got smaller
* _I forgot a critical UX piece._ Instructions! I had not factored in any time to build out instructions. My initial playable version didn't have them and was derided by friends for leaving that out. The ones who knew code didn't even want to bother looking at the source to find the controls.

## The Ugly

* Unless you're just screwing around to kill an hour on the train like I was, The DOM is indeed a dumb place to make a game. It's like bringing a scooter to ride the _Tour de France._
* Due to its bumpiness, I got a tiny bit of motion sickness by the time I got off the train. However, it felt like something I would get used to if I did this every day.
* Though the goals did not start out that way, this started to [feel like performance art with a tiny audience](http://www.youtube.com/watch?v=O2NVmBfKQf4 "This guy is more talented than I am, but most people still don't care.").

## _Redux?_

If I had to do this all over again:

* As part of my _mise en place_, I'd look for and then learn a _tiny and fast_ library that uses `<canvas>` (ideally with basic game or timer management.)
* In the discipline of practice, I would write more quick prototypes (main game logic, understanding the glaring edge cases) of the important pieces of the game in the days before the "event."

[ender]:http://ender.no.de "Ender JS"
[sublime]:http://www.sublimetext.com/ "Sublime 2 Text Editor"
[qwery]:https://github.com/ded/qwery "Qwery: A Tiny CSS Selector Engine"
[underscore]:http://documentcloud.github.com/underscore/ "Underscore JS"
[github]:http://github.com "Github!"
[dominvaders]:http://otanistudio.github.com/dominvaders "DOM Invaders!"
