---
layout: post
title: BlocJams
thumbnail-path: "img/blocjams.png"
short-description: Build a music streaming service.

---

{:.center}
![]({{ site.baseurl }}/img/bloc_jams_big_screen_max_width.png)

## Explanation

The way we consume media has changed quickly because of the internet. Rather than buy an album from one of our favorite bands, we're able to just buy a single from them. Or buy a song from a soundtrack, instead of the whole cd. Now with services like Spotify we're able to just stream the songs directly to our computer or phone.

Not to be left out of the growing market, we set out to build our own streaming service, it will be unlimited streaming, available on on mobile platforms, and completely ad free.

## Problem

Since the app is ad free, I don't need to clutter it with a lot of decoration. After a clean landing page, we'll have a simple interface of album covers, and from there, just a track listing for every album. We'll give the user the ability to play any track they want, select the previous, or the next track as often as they'd like, and with the addition of a play bar, they can skip forward in the song.


## Solution

I don't need to create user profiles, since there's no limit on plays, or album choice, there is no need to validate users. Just going to the album collection screen will be enough to start playing music. The set up of the landing page was made with simple CSS, I wanted to call out the main selling points of the service, and after that we went on to the "Collection" screen.

Every album has it's own page, but I didn't want to have static pages for every album, so I created a script that could dynamically generate as many album displays as needed.

{% highlight ruby %}
var buildCollectionItemTemplate = function() {
    var template =
     '<div class="collection-album-container column fourth">'
   + '  <img src="assets/images/album_covers/01.png"/>'
   + '  <div class="collection-album-info caption">'
   + '    <p>'
   + '      <a class="album-name" href="album.html"> The Colors </a>'
   + '      <br/>'
   + '      <a href="album.html"> Pablo Picasso </a>'
   + '      <br/>'
   + '      X songs'
   + '      <br/>'
   + '    </p>'
   + '  </div>'
   + '</div>'
   ;
{% endhighlight %}

we'll iterate over the albums in our collection, and the song list will populate as long as a track is detected.

Since every song needs a player and volume bar on the screen, I created the code on the "album" view. Through the use of event handlers and styled with simple CSS, we wrote a **`clickHandler()`** to deal with play and pause functions.



## Results

While I optimized the app to be used on mobile devices, it also needs to look good on big computer screens. My setting the viewport, and adding a max-width container, we set the site to look good on any screen size.

{% highlight ruby %}
@media (min-width: 640px) {
    html { font-size: 112%; }

    .column {
        float: left;
        padding-left: 1rem;
        padding-right: 1rem;
    }

    .column.full { width: 100%; }
    .column.two-thirds { width: 66.7%; }
    .column.half { width: 50%; }
    .column.third { width: 33.3%; }
    .column.fourth { width: 25%; }
    .column.flow-opposite { float: right; }
}
{% endhighlight %}

Because of the few needs of the app, there wasn't too much code needed. Some html for a couple of pages, and a couple of functions and scripts outlining the rules for albums, play, and volume bars, some JavaScript to dictate how we play songs; and the app was ready for release.

We populated our app with [Buzz music library](http://buzz.jaysalvat.com/).

## Conclusion

With an attractive purple color scheme, thin sans-serif fonts, and clean graphic design, our site looks modern and appealing.

Having unlimited skips, and the ability to listen to any specific part of the song, all while remaining ad free, is what sets our service apart from other music streaming platforms.
