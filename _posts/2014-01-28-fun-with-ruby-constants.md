---
title: Ruby Constants
author: Kieran Andrews
layout: post
permalink: /2014/01/fun-with-ruby-constants/
image:
  - 
categories:
  - Development
  - Ruby
---
I was doing some refactoring recently and made some interesting discoveries about how constants work in ruby. 

What tripped me up was how much of a mess this code made:

<pre name="code" class="ruby">module Greetings
  COMMON_GREETINGS = { "hello" => "Hello!", "goodbye" => "Good bye." }
end

class Greetings::Welcome
  GREETINGS = COMMON_GREETINGS.merge! { "welcome" => "Welcome" }
end

class Greetings::Christmas
  GREETINGS = COMMON_GREETINGS.merge! { "hoho" => "Ho Ho, Merry Christmas" }
end
</pre>

Can you spot the problems here? The first obvious one is merge with a bang, and the other I will explain below.

**What is a constant?**

Constants in ruby are anything starting with a capital letter. So class names are constants as well as all capital variables.

<pre name="code" class="ruby">MAX_EXECUTION_TIME = "60"</pre>

Constants aren&#8217;t completely similar in other language. For example in Java and PHP you cannot re-assign or change a constant. In ruby you can:

<pre name="code" class="ruby">2.0.0-p353 :001 > GREETING = "hello"
 => "hello" 
2.0.0-p353 :002 > GREETING = "goodbye"
(irb):2: warning: already initialized constant GREETING
(irb):1: warning: previous definition of GREETING was here
 => "goodbye" 
2.0.0-p353 :003 > GREETING
 => "goodbye" 
</pre>

Now you do get a warning, but its not an error and will not stop you from continuing. In the first example, the merge! actually modified the original constant so this was applied too all other classes using this constant.

There is one thing you can do if you want to ensure that the Object that the constant holds will not be modified, and that is by using the method freeze.

http://ruby-doc.org/core-2.1.0/Object.html#method-i-freeze

<pre name="code" class="ruby">2.0.0-p353 :001 > GREETING = "goodbye"
 => "goodbye" 
2.0.0-p353 :002 > GREETING.freeze
 => "goodbye" 
2.0.0-p353 :003 > GREETING &lt;&lt; " and hello"
RuntimeError: can't modify frozen String
	from (irb):3
	from /home/kieran/.rvm/rubies/ruby-2.0.0-p353/bin/irb:12:in `&lt;main>'
</pre>

But as you can see below, the Constant is still able to be re-assigned (but still gives us the warning).

<pre name="code" class="ruby">2.0.0-p353 :004 > GREETING = "goodbye and hello"
(irb):4: warning: already initialized constant GREETING
(irb):1: warning: previous definition of GREETING was here
 => "goodbye and hello" 
</pre>

As pointed out by Andrew, you can freeze the class constant that an object refers to which will stop it from being modified.

<pre name="code" class="ruby">class Foo
BAR = 1
end

# Works
class Foo
BAR = 2
end

Foo.freeze

# Doesn’t work
class Foo
BAR = 3
end
</pre>

Some other useful things about class constants is how easily they can be accessed. Constants defined in a class can even be reached without creating an instance of the class. You can even dynamically call the constant if you have a reference to the Class variable that contains the constant. For example:

<pre name="code" class="ruby">irb(main):005:0> class Work
irb(main):006:1> JOB = "Gardening"
irb(main):007:1> end
=> "Gardening"
irb(main):008:0> work = Work
=> Work
irb(main):009:0> work::JOB 
=> "Gardening"
</pre>

Im still not certain on how useful constants are for settings that never change but I prefer using them to class methods that re-define hashes every time they are called or yaml files. They can sometimes make testing easier and other times harder. 

Do you use constants much and how do you use them? Reply in the comments below.