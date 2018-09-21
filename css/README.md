# Efficient CSS tips
The priority of CSS selectors is based on the speed of rendering of each selector.

CSS selector priority:

1. ID, e.g. #header
2. Class, e.g. .promo
3. Type, e.g. div
4. Adjacent sibling, e.g. h2 + p
5. Child, e.g. li > ul
6. Descendant, e.g. ul a
7. Universal, i.e. *
8. Attribute, e.g. [type="text"]
9. Pseudo-classes/-elements, e.g. a:hover

**Rendering**

The way CSS processors render selectors is by first looking at the key selector - the last one on the right - and finding all elements which match it's rule. From thereon CSS processors go up in the DOM tree filtering the found results with each selector on the left. So a heavy selector - like **figure figcaption .social a** will check for all anchors on the page, then filter out those which don't belong to an element with .social class, then filter for figcaption, and then for figure.

A more efficient way of writing CSS selectors would be to set a class attribute to the specific elements we want to style. The class selector is quick and in this way the processor works with way fewer elements and possibly ( depending on your rule ) will not need to filter them.

Based on how big is your website you may not notice any visible change in rendering time, but on some occasions - this can visibly improve the loading time.

On the other hand good design suggests not to add unnecessary classes to your html, so best way is to keep a balance between clean markup and efficient CSS.

# CSS tricks

The CSS :nth-of-type selector, selects the element which is from the specified type, and is either the nth of that type or it satisfies a given formula.
The parameters of the selector can be
    :nth-of-type(2) which would select the 2nd element,
    :nth-of-type(2n) which would select all the elements whose index is a magnitude of 2,
    :nth-of-type(an + b) which would select all elements whose index is the result of of the given formula, where n starts from 0 and cycles up, and {a,b} are integers,
    :nth-of-type({odd, even}) would select either odd or even elements depending on the parameter.

The interesting stuff now comes from the following example.
You can try running this in a browser and see how it works. This may just be a current implementation bug, as I saw no formal specification of this.
The nth-of-type counts all elements that *appear* as elements from this type, even though they aren't exactly. I.e. it does a fuzzy match.
In the same time though it only applies the styles to the elements which are perfectly matched. Though it counts all of them.

```
<!DOCTYPE html>
<html>
<head>
<style>
.asd:nth-of-type(2n) {
    background: red;
}
</style>
</head>
<body>

<p class="asd.counted-though-it-is-different">The first paragraph.</p>
<p class="asd">The second paragraph.</p>
<p class="asdcountingthirdparagraph">The third paragraph.</p>
<p class="asd--counted-but-style-not-applied-cause-it-is-not-perfect-match">The fourth paragraph.</p>
<p class="asd-again-counted">The fifth paragraph.</p>
<p class="asd">The sixth paragraph.</p>
<p class="asdcountingseventhparagraph">The seventh paragraph.</p>
<p class="asd">The eight paragraph.</p>
<p class="asd">The ninth paragraph.</p>

</body>
</html>
```

## Sources

[Writing efficient CSS selectors](https://csswizardry.com/2011/09/writing-efficient-css-selectors/)

# How does CSS measure distance?

There are several ways to specify distance with CSS, but generally they can be separated in relative and absolute units.

__Relative CSS units__:
Name         |    Definition            |
|------------|--------------------------|
|  unit      |    relative to           |
|  em	     |    font size of the element           |
|  ex	     |    x-height of the element’s font           |
|  cap	     |    cap height (the nominal height of capital letters) of the element’s font           |
|  ch	     |    average character advance of a narrow glyph in the element’s font, as represented by the “0” (ZERO, U+0030) glyph           |
|  ic	     |    average character advance of a fullwidth glyph in the element’s font, as represented by the “水” (CJK water ideograph, U+6C34) glyph           |
|  rem	     |    font size of the root element           |
|  lh	     |    line height of the element           |
|  rlh	     |    line height of the root element           |
|  vw	     |    1% of viewport’s width           |
|  vh	     |    1% of viewport’s height           |
|  vi	     |    1% of viewport’s size in the root element’s inline axis           |
|  vb	     |    1% of viewport’s size in the root element’s block axis           |
|  vmin 	 |    1% of viewport’s smaller dimension           |
|  vmax 	 |    1% of viewport’s larger dimension           |


Child elements do not inherit the relative values as specified for their parent; they inherit the computed values.

__Absolute CSS units__:

| unit  | name	                     |  equivalence |
| ------|----------------------------|-------------------|
| cm	  |  centimeters             | 1cm = 96px/2.54    |
| mm	  |  millimeters             | 1mm = 1/10th of 1cm    |
| Q	      |  quarter-millimeters     | 1Q = 1/40th of 1cm    |
| in	  |  inches                	 | 1in = 2.54cm = 96px    |
| pc	  |  picas                	 | 1pc = 1/6th of 1in    |
| pt	  |  points                	 | 1pt = 1/72th of 1in    |
| px	  |  pixels                	 | 1px = 1/96th of 1in    |


## Sources:
[CSS Values and Units Module Level 4
W3C First Public Working Draft, 14 August 2018](https://www.w3.org/TR/css-values/#lengths)

__TODO:__

Write about the CSS px definition being the smallest visible line, hence different on different
devices.

https://www.w3.org/Style/Examples/007/units.en.html
