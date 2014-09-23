---
title: PHP Debugging
author: Kieran Andrews
layout: post
permalink: /2012/08/php-debugging/
categories:
  - Uncategorized
---
Recently while working on a particular project we had some strange errors that came up. In the usual php like way, the error messages where not very helpful and didn&#8217;t allude to what the actual problem was. Have you seen an error like this before?

**Headers Already Sent on line 392  
**

**Invalid argument supplied for foreach()**&#8230;

Well, this handy functionality that I discovered in php made my life easier.

`var_dump(debug_backtrace()); die;`

I placed this right before the code that was complaining, and it allowed me to see where this function was being called from. I was then quickly able to fix the problem and be on my merry way.