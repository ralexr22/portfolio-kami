---
layout: post
title: BlocJams (Angular)
thumbnail-path: "img/blocjams_angular.png"
short-description: Take our music streaming platform, BlocJams, and update it with Angular.

---

{:.center}
![]({{ site.baseurl }}/img/blocjams_angular.png)

## Explanation

I previously built a music streaming service to go up against major apps like Spotify and Apple Music. It wasn't code heavy, needing only a couple of pages, and a few rules to dictate music playback. Since we don't need a lot of code to load when navigating between pages, our [BlocJams](http://127.0.0.1:4000/main/portfolio/blocjams/) app was perfect for creating modules to handle our streaming service.

## Problem

While I was able to write a small number of lines of code to control the app, many of it's functions could be faster executed by using [AngularJS](https://angularjs.org/).

I could take the existing ideas and transform them into just a few controllers and use Angular's services to make my code run smoother as a single page application. Instead of outlining html and javascript rules for every page, I can make one module to contain the code I want for the different parts I may need on a page.


## Solution

Instead of using JQuery's `onHover` and `offHover` functions, we'll just declare the actions using `ngShow`

{% highlight ruby %}
<td class="song-item-number">
     <span ng-show="!playing && !hovered">1</span>
     <a class="album-song-button" ng-show="!playing && hovered"><span class="ion-play"></span></a>
     <a class="album-song-button" ng-show="playing"><span class="ion-pause"></span></a>
 </td>
{% endhighlight %}

We dictated that when the song is **not** playing *and* the mouse is **off** hover, we'll show the song number. The play button will show when the is **not** playing *and* the mouse is **on** hover. Whenever the song plays, we'll display the pause button.

The player and volume bars were created with a similar template which I included in the album view. I created services for the albums, the song player, and the player bar in my app, they were then injected as dependencies in my album view.

## Results

Most of the CSS remained the same, the main changes came in javascript. I configured the routing with [UI-Router](https://ui-router.github.io/ng1/) and with one of it's component's I was able to configure states.

Rather than have code on each individual page, I created controllers, and templates that dictated how I wanted parts of my app to work, making sure to include them in the new views for each page.

## Conclusion

With less code to load, our site now loads faster and runs quicker, letting us get to the music even faster. I kept the same look, and we still access our music collection the same way, so there's no discernible difference in the users' experience.
