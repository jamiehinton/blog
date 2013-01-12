---
layout: post
title: "JavaScript 'for loop' Performance"
date: 2013-01-12 18:23
comments: true
categories: [JavaScript, Optimisation]
---
I have read about optimising the performance of for loops in JavaScript a number of times but for the first time today I actually remembered to write one in the correct way. 

To compound this learning I thought that I would write this blog post and also hopefully get others to remember this optimisation too.

Take this for loop as an example:

{% codeblock %}
var array = new Array();
array[0] = "jibble";
array[1] = "flibble";
for(var i = 0; i <= array.length; i++){
	console.log(array[i]);
}
{% endcodeblock %}

All looks straight forward enough and probably what we have written many times. The problem is that the array.length will be evaluated on every itteration of the loop. This would be compounded if we had a function there that was doing some other intensive process.

There are a number of ways to rectify this but they generally resort to the same principle, create a variable.

Create one inline:
{% codeblock %}
for(var i = 0, l = array.length; i <= l; i++){
	console.log(array[i]);
}
{% endcodeblock %}

Or outside the for loop:
{% codeblock %}
var l = array.length
for(var i = 0; i <= l; i++){
	console.log(array[i]);
}
{% endcodeblock %}

They both result in the same one but you may find one more readable than the other.

There are plenty of other ways to get even more performance from loops in JavaScript. Just take a read of [this article](https://blogs.oracle.com/greimer/entry/best_way_to_code_a).

###Update
I really should have provided benchmarks to prove the difference. Well - I have done now:
[jsFiddle sample](http://jsfiddle.net/B8Rer/7/)

In Chrome on OS X with an array with a size of 9999999 took 16 millisecond the slow way and 13 millisecond the fast way.

As you can see it's not going to make a huge difference to the JavaScript you write. Basically - these metrics aren't worth much in the real world as it matters most what you are doing in the upper limit computation. 

They do however prove that the fast way example actually is faster ;)

