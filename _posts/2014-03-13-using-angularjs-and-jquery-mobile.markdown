---
layout: post
status: publish
published: true
title: Using AngularJS and jQuery Mobile
author: Kyle
author_login: 0not
author_email: unclekyky@gmail.com
wordpress_id: 42
wordpress_url: http://0not.net/?p=42
date: '2014-03-13 21:08:07 -0600'
date_gmt: '2014-03-13 21:08:07 -0600'
categories:
- Web Development
tags:
- angular
- angularjs
- jquery mobile
- jqm
comments: true
---
UPDATE: Well, I was hasty. What I say here is true, but offering it as a solution is incomplete. I have run into some problems by loading Angular then jQuery Mobile. Specifically, if AngularJS is loaded first, it does not ever get change events on radio buttons. If jQM is loaded first, the form works properly. Apparently, there is a bit more work that needs to go into finding a solution. It is a bummer that <a href="https://github.com/angular-widgets/angular-jqm" target="_blank">angular-jqm</a> is no longer under development.

UPDATE 2: I should really write a new post explaining this. The solution I have found is to load jQuery, AngularJS, and jQuery Mobile, *in that order!* This way, Angular runs before jQM, but it doesn't get locked out of the events (as explained in the previous UPDATE).

-----Original-----
Skip to <a href="#solution">the solution</a>, if that's all you're interested in.

<h2 id="problem">The Problem</h2>

At work we have a product that we now want to offer in a more mobile friendly environment. I was tasked with determining which libraries we should use. We were going to use jQuery Mobile for sure, but we needed something for templating. In the past we've used smarty and done all template work on the server-side. We wanted to steer clear of smarty and so the choice was either do "templates" with plain PHP, or use a JavaScript client-side template engine. I am a big proponent of separating logic and presentation (to an extent; I'm not a purist).

I experimented with several different libraries such as <a href="http://olado.github.io/doT/index.html">doT.js</a>, <a href="http://leonidas.github.io/transparency/">Transparency</a>, and <a href="http://akdubya.github.io/dustjs/">dust</a>. All of them have their pros and cons, but out of those three, doT fit the bill the most. I hadn't previously considered AngularJS, since I didn't think we needed two full blown frameworks, but slowly the idea of using it crept up on me. We use it on another related project, and it's always great to be able to share talent.

AngularJS has several very nice features, like data binding, services/factories/providers, and directives. Mainly, we wanted its data binding and built-in control directives (like `ng-repeat`). It offers a lot of features that we don't need, however. The great thing about AngularJS is its modularity. For example, we are letting jQM handle routing (since that's one of its strengths), so we won't use Angular's routing provider. No problem! Just don't include angular-route(.min).js.

Wondering how to get jQM and AngularJS to work well together, I found an article by Simon at simonguest.com called<a href="http://simonguest.com/2013/04/08/jquery-mobile-and-angularjs-working-together/" target="_blank">jQuery Mobile and AngularJS Working Together</a>. He proposed that jQM should be loaded first, and then Angular. If he didn't, he "found that loading AngularJS first led to some interesting (and annoying!) UI functionality." I have found the opposite. In fact, I am writing this post to clarify a comment I left on his blog. Hopefully, he'll read this and offer more insight into the nature of the "interesting... UI functionality" that he just briefly mentioned.

<h2 id="solution">The Solution</h2>

The correct (at least in my case) load order is to load AngularJS, then jQuery Mobile. The simple reason is that AngularJS will ignore jQuery Mobiles data- attributes, but jQM doesn't know what to do with unexpanded Angular directives. Let's take, for example, the situation I discussed in the <a href="http://simonguest.com/2013/04/08/jquery-mobile-and-angularjs-working-together/#comment-17187" target="_blank">comment</a> on Simon's blog.

```html
<ul data-role="listview" data-inset="true">
    <li data-role="list-divider"></li>
    <li ng-repeat-start="prod in products">{{prod}}</li>
    <li ng-show="$index == 0" data-role="list-divider" ng-repeat-end></li>
</ul>
```

Let us define our two cases as: A) jQM first, then Angular and B) Angular first, then jQM.

In case A, jQM will see an unexpanded `ng-repeat-start/end`. It will apply styles to the list elements, such as `ui-first-child` and `ui-last-child`. The first `list-divider` in the ul is fine to be labeled with class `ui-first-child`. However, the second `list-divider` (with the conditional statement), should not be labeled as `ui-last-child`, because there will possibly be more products later. If there are more products, then this `list-divider` will _never_ be the last child. Here is a slice of the left-most side of a three product list:

<a href="/images/angular/Screen-Shot-2014-03-13-at-3.15.56-PM.png"><img class="alignnone size-thumbnail wp-image-59" alt="jQM and AngularJS Wrong" src="/images/angular/Screen-Shot-2014-03-13-at-3.15.56-PM-56x150.png" width="56" height="150" /></a>

For case B, AngularJS will run first and expand the `ng-repeat` directive. That modified DOM is what jQM sees. Now jQM can appropriately style the elements. Here is the same slice, but with Angular loaded first:

<a href="/images/angular/Screen-Shot-2014-03-13-at-3.16.30-PM.png"><img class="alignnone size-thumbnail wp-image-60" alt="AngularJS and jQM Correct" src="/images/angular/Screen-Shot-2014-03-13-at-3.16.30-PM-48x150.png" width="48" height="150" /></a>

<h2 id="conclusion">The Conclusion</h2>

In summary, here is what I am doing (with no adverse effects, so far):


* At the bottom of `body`, load AngularJS and then jQM
* Use jQM for routing (which is the default, as long as you don't include ngRoute)


Thanks for reading. Comment below if you have anything to add!
