#Advanced CSS Selectors

##Introduction

This past January, I gave a presentation at work on advanced CSS selectors, introducing the team to a number of selectors they hadn't yet used, in order to ensure the everyone had been made aware of the more advanced possibilities of what can be achieved using CSS. 

*This is an adaptation of that presentation.*

This article assumes that you're already familiar with constructing simple `id` and `class` selectors, and covers more advanced selectors that may be created when combining these simple selectors.  

##Table of Contents
1. ####Hierarchical Selectors
   1. Descendant
   2. Child
   3. Adjacent
   4. Sibling
2. ####Attribute Selectors
   1. Has Attribute
   2. Attribute Equals
   3. Attribute Contains
   4. Attribute Starts With
   5. Attribute Ends With
   
- - - 
##Hierarchical Selectors
Hierarchical selectors allow elements to be selected depending on how it is positioned in relation to another element. 

####Descendant Selector
The descendent selector is represented by a space between two selectors.

	#parent .child { color: #FFF; }

This will select all of the elements with the `class` **child** that descend from the element with an ID of **parent**. 
	
Besides the type, ID, and class selectors, this is probably the most popular type of selector.  A slightly more performant child selector is available for when only one child level must be searched. This child selector is outlined next. 

####Child Selector
The child selector is represented by a '>' character between selectors and allows an element to be selected if it is a direct descendant of a parent element. 

	#parent > .child { color: #FFF; }

Some developers I know tend to skip this selector, even when they are only selecting direct children. There is a performance increase when using this selector appropriately, instead of the descendent selector.

####Adjacent Selector
The adjacent selector is represented by a '+' character between selectors and allows an element to be selected depending on whether or not it's previous sibling node matches the first part of the selector.

	.apple + .orange { display: none }
	
This rule will hide an element containing the `orange` class so long as it's immediately preceded by an element with the `apple` class, provided that both elements share the same parent. 

	<div class="orange"></div>
	<div class="apple"></div>
	<div class="orange"></div> <!-- rule above only selects this one -->
	
In this example, our selector will only select the second element with the `orange` class, as it is the only one preceded by the element with an `apple` class. 

####Sibling Selector

The sibling selector works much like the adjacent selector, but allows any element to be selected based on **any** of it's previous siblings. This selector uses the '~' character between two selectors.

	.apple ~ .orange { display: none; }

This will allow any element with the `orange` class to be selected as long as it has a **preceding** sibling with a class of `apple`

	<div class="apple"></div>
	<div class="orange"></div> <!-- rule selects both -->
	<div class="orange"></div> <!-- rule selects both -->

- - -
##Attribute Selectors
While hierarchical selectors are the most popular selectors, there also exists great functionality in selecting elements based on the value of one of the element's attribute values. There exist a handful of these selectors.

####Has Attribute
The 'Has Attribute' selector, as I call it, allows you to select an element based simply on whether or not that element has a the specified attribute. 

These rules are in a slightly different format:

	div[id] {  color: #F00; }
	
This rule will match any `div` element that has an `id` attribute.

####Equals
The equals attribute selector allows you to select an element when the value of an elements attribute matches a provided pattern. 

For example, the following rule will select any `<a>` tags that have a title attribute equal to 'Home' 

	a[title="Home"] { font-weight: bold; }
	
The ID selector can also be written using this syntax: 

	div[id="some-id"] { border: 1px solid black;  } 
	
	/* is equivalent to */
	
	div#some-id  { border: 1px solid black;  }
	
These rules can also be written without the tag selector, too:
	
	[id="some-id"] { border: 1px solid black;  }
	
	/* is equivalent to */
	
	#some-id { border: 1px solid black;  }

####Contains

The attribute contains selector allows a match to be made on only a substring of the value of an element's attribute. This is much like the **equals** selector, but uses the operator `*=` in place of `=`. 

The following rule will select any `div` that has an `id` containing a dash (`-`).

	div[id*="-"] { font-weight: bold; } 
	
	
####Starts With
This selector operates much like you'd expect, matching a substring of an attribute's value, provided that the substring occurs at the beginning of the attribute's value. This works like the previous examples, using instead the `^=` operator. 

	#parent > div[id^="cs-"] { border: none; }
	
This rule matches any `div` that is child to `#parent` who have an `id` with a prefix of `cs-`.
	

####Ends With
This selector operates much like you'd expect, matching a substring of an attribute's value, provided that the substring occurs at the end of the attribute's value.

	#parent > div[id^="Btn"] { border: none; }
	
This rule matches any `div` that is child to `#parent` who have an `id` ending in `Btn`. \