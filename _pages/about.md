---
permalink: /
# title: "Welcome!"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<style>
   #columns {
       width: 770px;
       overflow:auto;
   }

   #columns .column {
       float: left;
   }

   #columns .date {
       width: 160px;
   }

   #columns .description {
       width: 540px;
   }

        /* Set width length for the left, right and middle columns */
    #columns .left {
    width: 50%;
    }
    
    #columns .right {
    width: 50%;
    }

    #columns .row:after {
    content: "";
    display: table;
    clear: both;
    }
</style>

<span style="color: #7e7f7a; font-family: American Typewriter, serif; font-size: 1.7em;">Welcome!</span>

I am a computational science PhD student in a joint doctoral program between [San Diego State University](https://www.sdsu.edu/) and [University of California Irvine](https://uci.edu/). My research interests include developing and utilizing mathematical and computational modeling techniques for biological applications. The primary focus of my doctoral research is in computational developmental toxicology. I am under the primary advisement of [Dr. Uduak George](https://georgelab.sdsu.edu/) along with [Dr. Karilyn Sant](https://publichealth.sdsu.edu/people/karilyn-sant/) and [Dr. Pierre Baldi](https://www.igb.uci.edu/~pfbaldi/). For more information about my research please visit my research page!

<span style="color: #7e7f7a; font-family: American Typewriter, serif; font-size: 1.7em;">Education</span>

<div id="columns">
    <div class="date column">
        <b> 2020 - present </b>
    </div>
    <div class="description column">
        <b>Computational Science</b>, <font color="#7e7f7a">Doctor of Philosophy</font>
        <br><i>San Diego State University and University of California Irvine</i>
    </div>
</div>

<div id="columns">
    <div class="date column">
        <b> 2019-2020 </b>
    </div>
    <div class="description column">
        <b>Applied Mathematics</b>, <font color="#7e7f7a">Graduate Coursework</font>
        <br><i>San Diego State University</i>
    </div>
</div>

<div id="columns">
    <div class="date column">
        <b> 2015-2019 </b>
    </div>
    <div class="description column">
        <b>Applied Mathematics</b>, <font color="#7e7f7a">Bachelor of Science, <i>cum laude</i></font>
        <br><i>San Diego State University</i>
    </div>
</div>
<br>
<span style="color: #7e7f7a; font-family: American Typewriter, serif; font-size: 1.7em;">Featured</span>
<br>
<hr>
<div id="columns">
  <div class="column left">
        <span style="font-family: American Typewriter, serif; font-size: 1.2em;">2023 SDSU CSRC ACSESS</span>
      <br>
        <span>Recently, I presented at the annual SDSU Computational Science Research Center <a href="https://sites.google.com/sdsu.edu/acsess2023">ACSESS Event</a>. For this meeting, I presented on some of my recent work in a quick 5 minute presentation. See below for my mini-presentation! </span>
  </div>
  <div class="column right">
    {% include youtube-small.html id="65kLhZoQy_I" %}
    <br>
  </div>
</div>
<hr>
<div id="columns">
  <div class="column left">
      <span style="font-family: American Typewriter, serif; font-size: 1.2em;">Tweeting...</span>
      <br>
      <span>Check out my twitter page for some recent tweets, thoughts, and events.</span>
  </div>
  <div class="column right">
    <a class="twitter-timeline" data-height="400" data-width="400" data-theme="dark" href="https://twitter.com/ashleyvschh?ref_src=twsrc%5Etfw">"Tweets from @ashleyvschh"</a> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
    <br>
  </div>
</div>
<hr>

{% include archive-single.html %}