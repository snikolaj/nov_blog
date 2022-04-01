---
layout: page
title: "About Me"
permalink: /about/
---

I'm Stefan Nikolaj, a <span id="age"></span> year old student from Macedonia. I like programming, video games, electronics, history and many other things. But I'm interested in many things, and know a lot about fun areas like retro computers, the history of pop music, synthesizers, development of tanks and other armored vehicles, 6th century European history and many other things.

I have used all 3 major operating systems, and currently use both Manjaro Linux and Windows 10. I love C and C++, but have made interesting things in every major programming language. The Java Processing framework in particular is one I love. BASIC is also an awesome language and I have made a couple of videos about it. In the past year I've also been doing many things with Arduinos and microcontrollers and I love it. I've also been looking to buy some retro computers, so if you're in the Balkans and have a retro computer (especially domestic Yugoslav ones), please contact me.

I don't have one favorite video game, but there are many I love. More notable games I love are Battlefield 1, World of Tanks, the Command and Conquer series, the Total War series, the Men of War series, the Fallout series and many more.

This blog is made in Jekyll, with sparse Javascript and CSS, thus each page only comes around to a couple of kilobytes in size. Eco-friendly indeed!

<h3 id="contact">Contact me</h3>
You can contact me through:
- [Github](https://github.com/snikolaj)
- [Youtube](https://www.youtube.com/channel/UCJxzNR_M2Urx6u30l7i-8uQ/)

<script>
    /* SET MY CURRENT AGE */
    var birthDate = new Date(2004, 2, 14); // (Date counts months from 0-11, so 2 is March)
    var currentDate = new Date(); // returns current date
    var diff = new Date(currentDate.getTime() - birthDate.getTime()); // difference between current date and birth date referenced to 1970
    document.getElementById("age").innerHTML = (diff.getUTCFullYear() - 1970); // remove the 1970 adjustment
</script>