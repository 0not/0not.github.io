---
layout: post
status: publish
published: true
title: 'Pre-mortem: Using AngularJS and jQuery Mobile Together'
author: Kyle
author_login: 0not
author_email: unclekyky@gmail.com
wordpress_id: 74
wordpress_url: http://0not.net/?p=74
date: '2014-10-14 23:23:33 -0600'
date_gmt: '2014-10-14 23:23:33 -0600'
categories:
- Web Development
tags: []
comments: true
---
# Or, how I wish this was a postmortem, but I'm still working on the project...

I feel like I am now the world's leading expert on using AngularJS and jQuery Mobile together. Then again, I am one of the very few poor fools who's actually tried. My advice: for the love of all that is good an right in the world (of which the code baby of Angular and jQM is not a part), please re-think whatever brought you to this page. I can whole-heartedly support using AngularJS. Or, if jQM is your thing, then go for it. But, if you want a mobile solution for AngularJS, _do not use_ jQuery Mobile (I have had plenty of success with <a href="http://getbootstrap.com/" target="_blank">Bootstrap</a> in other projects).

Please see my [first post](/web%20development/2014/03/13/using-angularjs-and-jquery-mobile.html) regarding this topic.

The main problem is that both frameworks want to be in charge. Yes, I said both _frameworks_, for both are indeed, self-professedly (and inherently), frameworks. This causes all kinds of problems.

If jQM loads first, it will parse the DOM, doing it's magic on lots and lots of uncompiled Angular directives. Then when Angular gets a turn, it will parse and compile its directives, but now they are not formatted properly. This is not what we do.

At my job, we're doing it the other way. Load AngularJS first. Let it do its thing. Then let jQM do its thing. (Note, that in both cases you can't use Angular's routing). On the surface this seemed fine. Once I got down to the nitty gritty, I realized that Angular will continue to modify the DOM, but jQuery Mobile won't recognize the change. Want to dynamically update a drop-down list? Great -- modify the model and then perform a jQuery Mobile $(".selector").selectmenu("refresh") inside a timeout. We have dozens of these cases throughout our codebase now. Not fun.

Maybe I'm an even bigger fool than it seems and I'm just missing something, but I hope not. If not, then I can confidently say I will never have to use jQM and Angular together again. Heck, I probably won't use jQM ever again anyway.
