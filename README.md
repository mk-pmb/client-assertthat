A Client Version of node-assertthat
===================================

This will be a client version of [node-assertthat][]

All function of the original are working fine. All tests of these functions a green.
For more information of these functions, have a look at node-asserthat.

But why did I take node-assertthat? Because it is very easy to write and to read. This is a kind of philosophy trough the whole framework.
I try to keep this, when i ad new functions. What would be easier than writing:
```
assert.that(actual, is.equalTo(expected));
```
Everybody knows what this is looking for.


Usage
=====

It's very easy to use this. Clone this projekt an run the `test.html`.
That's it!

You are able to add your own tests by doing a simple script include:
```
<script type="text/javascript" src="test/myTest.js"></script>
```

DOM Testing
===========

In my workflow with a project of my own I saw that I needed some DOM testing functions, too.
I first tried to start adding new functions in a `has.*` namespace. Those functions were not stable, but as I did my first tests, they turned out to kind of work, unitl now.

For more Information watch the issue. [:FIXME: find issue number and add link]

has.attribute("value")
----------------------

Use this test to look for attributes of DOM nodes.
At the moment it works with `has.class("value")` and `has.id("value")`. You can use it without testing for a value, too.
```
var actual = document.createElement("div");
…
assert.that(actual,has.class("myClass")); //checks if ther is a class with the value myClass in actual
assert.that(actual,has.id("myId")); //checks if ther is a id with the value myId in actual
assert.that(actual,has.class()); //checks if therer is a class attribute in actual
assert.that(actual,has.id()); //checks if therer is a class attribute in actual
```

Class name testing does not yet support multiple class names declared on the same element.
Negation has to be tested, too.

has.listItem
------------

If you want to check whether there is a textNode in you list, you can use `has.listItem("text")`.
You can use DOM element objects or strings with CSS selectors (actually, currently only # for IDs):
```
var actual = document.getElementById("actual");

assert.that(actual, has.listItem("text"));  //passes the test if actual is a list that has one item called 'text'
assert.that(actual, has.no.listItem("text"));  //passes if actual is a list an has no item called 'text'

//easier:
assert.that("#actual", has.listItem("text")); //passes the test if actual is a list that has one item called 'text'
assert.that("#actual", has.no.listItem("text")); //passes if actual is a list an has no item called 'text'
```

has.childTag()
--------------

Is working with both CSS selectors (to the extent described above) and with DOM element objects.
Use this function if you want to check if an element is a parant. ;-)

```
var actual = document.getElementById("actual");
var expected = document.getElementById("expected");

assert.that(actual, has.childTag(expected));
assert.that(actual, has.no.childTag(expected));

//but easyer:
assert.that("#actual", has.childTag("#expected"));
assert.that("#actual", has.no.childTag("#expected"));
```

A combination of both works, too.

has.childText()
---------------

Test if a node is a parent of a text node. Works equal to `has.childTag()`.
```
var actual = document.getElementById("actual");

assert.that(actual, has.childTag("text"));
assert.that(actual, has.no.childTag("text"));

//but easyer:
assert.that("#actual", has.childTag("text"));
assert.that("#actual", has.no.childTag("text"));
```

A combination of both works, too.

has.lengthOf(number, opt)
-------------------------

This is a powerful tool to check the number of tags inside another one.
You can only count child nodes:
```
assert.that(actual, has.lengthOf(7));  //passes if actual has exactly 7 child tags (not counting text nodes!)
assert.that(actual, has.no.lengthOf(7));
```

But you are able to count tags by name:
```
assert.that(actual,has.lengthOf(7, "li")); //passes if actual has exactly 7 list items
assert.that(actual,has.no.lengthOf(7, "li"));
```
Or you count all nested tags:
```
assert.that(actual,has.lengthOf(7, "all")); //passes if actual has got 7 listItems
assert.that(actual,has.no.lengthOf(7, "all"));
```
:FIXME: use `*` instead of `all`

In all cases shown above, for the `actual` parameter it is equivalent to pass either a DOM node object as or a CSS selector string (to the extent described above).

:FIXME: Try to use the CSS selector engine of [jsdom][] or jQuery.


 [node-assertthat]: https://github.com/goloroden/node-assertthat
 [jsdom]: https://github.com/tmpvar/jsdom
