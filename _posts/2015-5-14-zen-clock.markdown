---
layout: post
title:  "Zen Clock Project"
date:   2015-5-14
image: zen_clock.jpg
tags:
  - projects
  - portfolio descriptions
---

<p class="intro"><span class="dropcap">N</span>ow that I have finally gotten around to creating my blog, I have decided that my best course of action is to backlog my way through project descriptions.</p>

Because this is the first time I am posting on this blog, and really the first time I have ever blogged in any meaningful sort of way, I have decided to start with the smallest, easiest project that is in the [portfolio]("http://iampjt.com/#portfolio") on my website, [Zen Clock]("http://iampjt.com/projects/clock").

Before I get into the description of the Zen Clock, I should mention something that may have stuck out to you about this post, which is the date. The date that I put down for this post being written is May 14, 2015. The date today (as I am currently writing it) is in reality August 3, 2015. The reason for this, as I mentioned previously, has to do with backlogging my posts. I am doing this because I would rather have my posts in a more chronological (though approximate) time-frame and order so that everything is better organized and so I don't end up with a pileup of a bunch of posts all written on the same day talking about something that actually happened a while back.

# To the Point: Zen Clock
Zen Clock is the product of a particularly slow May afternoon sitting in Western Civ class pretending to pay attention to the discussion (sorry Mr. McAuliffe) while at the same time trying to find something on my laptop to fend off boredom.

Earlier that day I had come across an interesting subreddit: [/r/Cinemagraphs]("http://reddit.com/r/Cinemagraphs").

For those uninformed on the nature of cinemagraphs, here is the definition provided by the moderators of the subreddit:

<blockquote>
A cinemagraph is a high quality gif or video that is very smoothly looped. It's more than a well looped gif, though; it should be beautiful as a great photograph, evocative like a movie, and more alive than either. A great cinemagraph is wonderful art!
</blockquote>

Finding that I still had the tab in my browser open to /r/Cinemagraphs, I continued browsing them, and finally decided I wanted to create something that incorporated them.

Somehow, the idea of creating a browser homepage with cinemagraphs as the background came to me, and I went with it.

# Behind the Scenes
Zen clock is extremely simple. One HTML file, 111 lines, for a grand total of 2455 characters. For those that don't know that is very small.

But in the interest of due diligence, I will give some brief explanation of the code that makes Zen Clock tick (pun not intended).

Skipping over the file <head> and the messy CSS styling, we come to a div with the label "clock". Followed closely by the closing body tag. This may seem somewhat confusing, seeing as there is no code that seems to tell the browser how to display the clock, let alone the gif in the background.

Herein lies the trick: about 99% of this entire project relies on jQuery, a popular library for implementing Javascript. jQuery, put simply, makes working with Javascript easier, and therefore makes the developer's life easier. Which is good.

### So how exactly does the page run?

This script is actually fairly simple to understand, even for someone with little to no programming experience (one of the beauties of Javascript). Here is a brief breakdown of what it all means.

The function first runs when the window is loaded. This makes sure that the it will be called right away, so there is no waiting for the clock and background to show up.

{% highlight javascript %}
$(window).ready(function() {
  $('#loading').hide();
});
{% endhighlight %}

This is where the function actually begins to work, starting with getting the current time by calling the Date function, which is builtin to Javascript. It thens splits up the returned Date (which also includes the time in it) into different sections (hours, minutes, seconds).

{% highlight javascript %}
function displayTime() {
  var currentTime = new Date();

  var hours = currentTime.getHours();
  var minutes = currentTime.getMinutes();
  var seconds = currentTime.getSeconds();
  var meridiem = "AM";
{% endhighlight %}

The next section is the logic for the clock, which serves to convert the returned Date, which is in 24-hour time by default, to a more readable and standard 12-hour time. This is done by checking the value of the hours, minutes, and seconds in a series of 'if' statements (yes, there probably is a better way to do this), and if this logic determines that it is afternoon, the meridiem, which was set to "AM" when first declared is changed to "PM".

{% highlight javascript %}
if (seconds < 10) {
  seconds = "0" + seconds;
};
if (minutes < 10) {
  minutes = "0" + minutes;
};
if (hours < 10) {
  hours = "0" + hours;
};
if (hours >= 12) {
  hours = hours - 12;
  meridiem = "PM";
};
if (hours === 0) {
  hours = 12;
};

{% endhighlight %}


Now that we have the time in 12-hour format, all that is left to do is to display the clock, and set it to update every second.

{% highlight javascript %}
var clockDiv = document.getElementById('clock');

clockDiv.innerText = hours + ":" + minutes + ":" + seconds + " " + meridiem;
}

displayTime();

setInterval(displayTime, 1000);

function setBackground() {
var i = Math.floor((Math.random() * 6) + 1);
document.getElementById('bg').src = "img/" + i + ".gif";
}

setBackground();
setInterval(setBackground, 900000);
});

{% endhighlight %}

Finally, the background is set by choosing a random gif from my image assets file and display it at full width and height as the background for the page.

{% highlight javascript %}
function setBackground() {
  var i = Math.floor((Math.random() * 6) + 1);
  document.getElementById('bg').src = "img/" + i + ".gif";
}

setBackground();
setInterval(setBackground, 900000);
});
{% endhighlight %}


<span class="dropcap">W</span>ell, this post has gotten longer then I expected, so I am going to wrap it up. More soon.

-PJT
