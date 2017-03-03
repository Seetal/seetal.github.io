---
layout: post
title: "BEM"
date: 2017-03-01T08:30:00.000Z
published: true
---

A little late to the party but I figured it’s about time I tried BEM. Having worked with a lot of existing projects and therefore legacy code over the last few years, I’ve had little chance to try any new css methodologies. Recently I started a smaller project so thought it was time to give BEM a try.

## What is BEM?

Block Element Modifier (BEM), is a naming convention for css and html classes which makes it easier to understand the relationship between elements of a component. 

The Block is a stand alone block or component on a web page. Element is a part of that block. Modifier is a different version of the Block or an Element. The syntax is:

{% highlight css %}
.block { }

.block__element { }

.block__element--modifier { }
{% endhighlight %}

This is probably better explained using an example.

<img src="/images/bem.jpg" class="contentImage" alt="Diagram explaining BEM" />

Imagine a list of products on an ecommerce site. Each product would be a block:

{% highlight css %}
.product { }
{% endhighlight %}

Each child element of the block would be the element and separated by 2 underscores: 

{% highlight css %}
.block__description { }
.block__price { }
{% endhighlight %}

Different versions of these would be modifiers, separated by 2 hyphens:

{% highlight css %}
.block__description--onSale { }
.block__price--onSale { }
{% endhighlight %}

The reason for the double hyphens and underscores is because its common practice for a single underscore or hyphen to be used in class names anyway, so using double for BEM means people don’t have to change their regular way.

One of the issues I had when starting out was if an element isn’t a direct child of the block then the class name will be very long: 

{% highlight css %}
.block__element1__childOfElement1__childOfChildOfElement1 { }
{% endhighlight %}

I figured this couldn’t be right so searched google for the answer which was actually very simple. An element thats isn’t a direct child of the block is still a child of the block so the class would still be:

{% highlight css %}
.block__element4LevelsDeep { }
{% endhighlight %}

## Some of the cool things about BEM

* Specificity is very low. Browsers read selectors from right to left, and not left to right. For example in the following, <span class="inlineCode">.product .details .price</span>, the browser would first match all instances of <span class="inlineCode">.price</span> then move up the dom and filter them to match <span class="inlineCode">.details</span> and then the same with <span class="inlineCode">.product</span>. The browser has to do a lot of work meaning it could affect performance. With BEM the css is applied via a single class meaning the page should render faster.
* All classes for any particular block are linked, meaning it should be easier for developers in the future to know exactly what the class does, well, as long as the classes have relevant names that is. 
* It follows the Don’t Repeat Yourself (DRY) concept of Object Orientated Programming. Each block is a self contained object so should be reusable.

## Some of the not so cool things about BEM

* Its not really the prettiest naming convention, the classes can have long names and make the code look quite ugly. But this isn’t really a problem once you get used to it, after all users won’t be seeing the code.
* For small sites it can be a little overkill. I used it on a website for a small martial arts club. About 10 page site, quite simple, no complex parts. At the moment I’m thinking I won’t use it on smaller sites again but I will test it in the coming months while editing the site to see if BEM makes it easier for me. 
* With BEM class names being quite long, this could increase the css file size but that will be minimal and with minification that will be reduced even more.

## BEM with SASS

I use sass to write my css, the <span class="inlineCode">&</span> in sass makes it easy to write BEM:

{% highlight scss %}
.product {
	border: 2px solid #ddd;
	&__description {
		font-size: 0.9em;
	}
	&__price {
		font-size: 1.5em;
		&--onSale {
			color: red;	
		}
	}
}
{% endhighlight %}

This will compile to:

{% highlight css %}
.product {
	border: 2px solid #ddd;
}
.product__description {
	font-size: 0.9em;
}
.product__price {
	font-size: 1.5em;
}
.product__price--onSale {
	font-size: 1.5em;
	color: red;
}
{% endhighlight %}


## BEM for the future

BEM is one of many methodologies for writing css, and from my initial experience I believe it will be very useful. It definitely isn’t the prettiest naming convention but that doesn’t really matter. Where I think BEM will excel is maintaining websites in the future.
