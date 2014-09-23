---
title: jQuery Scrolling Box
author: Kieran Andrews
layout: post
permalink: /2011/03/jquery-scrolling-box/
categories:
  - Uncategorized
tags:
  - development
  - jquery
---
I am currently working on a website that requires some scrollable elements on it. The design specification is to do away with the scroll bars to allow for a better more simplistic design. Now I remember this being done in the past in flash, but I wasn&#8217;t going to be using flash. So naturally I went out to find a jQuery solution. In most cases doing a google search or [stackoverflow][1] search finds some code that needs some tweaking and then away we go, but this time I couldn&#8217;t find anything! So I created my own and thought I would share it.

Go straight to the demo: <http://jsbin.com/azoji3>  
Full Source Code: <http://jsbin.com/azoji3/edit>  
An Example illustration:

[<img src="http://seekieran.com/wp-content/uploads/2011/03/example.jpg" alt="" title="example" width="148" height="185" class="alignnone size-full wp-image-98" />][2]  
I got my inspiration from this question: <http://stackoverflow.com/q/1193414/359736>

First up is the mousedown event to capture the clicking of the down arrow. This will call the function that will actually scroll down the div and it also keeps track of the mousedown.

<pre name="code" class="javascript">$('.dn').mousedown(function(event) {
    mouseisdown = true;
    ScrollDown();
}).mouseup(function(event) {
    mouseisdown = false;
});</pre>

This is where the fun comes in, this part is recursive (I know everyone loves recursion!). This is so you can hold down the mouse and keep it scrolling continuously. It will also check when it reaches the bottom.

<pre name="code" class="javascript">function ScrollDown(){

  //var topVal = $('.up').parents(".container").find(".content").css("top").replace(/[^-\d\.]/g, '');
  var topVal = $(".content").css("top").replace(/[^-\d\.]/g, '');
    topVal = parseInt(topVal);
  console.log($(".content").height()+ " " + topVal);
  if(Math.abs(topVal) &lt; ($(".content").height() - $(".container").height() + 60)){ //This is to limit the bottom of the scrolling - add extra to compensate for issues
  $('.up').parents(".container").find(".content").stop().animate({"top":topVal - 20  + 'px'},'slow');
    if (mouseisdown)
setTimeout(ScrollDown, 400);
  }</pre>

**Mouse scrolling**

Now I also wanted the user to be able to scroll the mouse and it scroll the content. To enable the detection of scrolling in jquery, it requires the library from here <http://github.com/brandonaaron/jquery-mousewheel>. Then I did the same scrolling action as above.

<pre name="code" class="javascript">$('.container').mousewheel(function(event, delta, deltaX, deltaY) {
   // console.log('mouse'+ delta, deltaX, deltaY);

  if(delta &lt; 0){ //Scroll down       var topVal = $('.up').parents(".container").find(".content").css("top").replace(/[^-\d\.]/g, '');     console.log('lol');     topVal = parseInt(topVal);     $('.up').parents(".container").find(".content").stop().animate({"top":topVal + (deltaY * 10)  + 'px'},'slow');   }     if(delta &gt; 0){ //Scroll up
      var topVal = $('.up').parents(".container").find(".content").css("top").replace(/[^-\d\.]/g, '');
    topVal = parseInt(topVal);
    $('.up').parents(".container").find(".content").stop().animate({"top":topVal - (-deltaY * 10)  + 'px'},'slow');
  }

});</pre>

I know its not the most optimized code and could do with some better selectors but I am very happy with it at the moment that it will do the job and be a part of this exciting website im working on. Feel free to make comments or ask questions, and suggestions are welcome and ill be updating this with any tweaks I can find.

 [1]: http://stackoverflow.com
 [2]: http://seekieran.com/wp-content/uploads/2011/03/example.jpg