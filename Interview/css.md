## In how many ways can a CSS be integrated as a web page?
- Inline: Style attribute can be used to have CSS applied HTML elements.
- Embedded: The Head element can have a Style element within which the code can be placed.
- Linked/ Imported: CSS can be placed in an external file and linked via link element.

## What pros and cons do External Style Sheets have?
pros:
- One file can be used to control multiple documents having different styles.
- Multiple HTML elements can have many documents, which can have classes.
- To group styles in composite situations, methods as selector and grouping are used.

cons:
- Extra download is needed to import documents having style information.
- To render the document, the external style sheet should be loaded.
- Not practical for small style definitions.

## What is CSS Box Model and what are its elements?
This box defines design and layout of elements of CSS. The elements are:

- Margin: the top most layer, the overall structure is shown
- Border: the padding and content option with a border around it is shown.  Background color affects the border.
- Padding: Space is shown.
- Content: Actual content is shown.

## How can the gap under the image be removed?
As images being inline elements are treated same as texts, so there is a gap left, which can be removed by:
`img { display: block ; }`

## Why is `@import` only at the top?
`@import` is preferred only at the top, to avoid any overriding rules. Generally, ranking order is followed in most programming languages such as Java, Modula, etc.

## What are Pseudo-class?
A CSS pseudo-class is a keyword added to a selector that specifies a special state of the selected element(s). For example, `:hover` can be used to change a button's color when the user hovers over it.

## How CSS style overriding works(What is specificity? How do u calculate specificity?)?
1. The basic css overriding for either internal / external css goes as follows: The css relating to corresponding elements, that is written at the latter has the highest priority, and it overrides those written at the top.
Here the 2nd one will override the first one.

2. The more specific rule will be considered. E.g. If there are two paragraph that's inside footer one with I'd value of copyright.

## How absolute, relative, fixed and static position differ?
`absolute`, is positioned relative to the nearest positioned ancestor (instead of positioned relative to the viewport, like fixed). However; if an absolute positioned element has no positioned ancestors, it uses the document body.

`relative`, is position an element relative to itself (from where the element would be placed, if u don't apply relative positioning). for example, if u set position relative to an element and set top: 10px, it will move 10px down from where it would be normally.

`fixed`, element is positioned relative to viewport or the browser window itself. viewport doesn't changed if u scroll and hence fixed element will stay right in the same position.

`static`, element will be positioned based on the normal flow of the document. usually, u will use position static to remove other position might be applied to an element.

## What are the differences between inline, block and inline-block?
`inline`, elements do not break the flow. think of span it fits in the line. Important points about inline elements, margin/ padding will push other elements horizontally not vertically. Moreover, inline elements ignores height and width.

`block`, breaks the flow and dont sits inline. they are usually container like div, section, ul and also text p, h1, etc.

`inline-block`, will be similar to inline and will go with the flow of the page. Only differences is this this will take height and width.

## How do you align a `p` center-center inside a div?
`text-align: center`will do the horizontal alignment but `vertical-align: middle` will not work here. there are couple of different ways to solve this problem and one of them are positioning. You make the parent as relative position and child as absolute positioning. And then define all position parameter as zero, width 50% and height 30%, margin as auto.
```
.parent{
  height: 100px;
  border: 2px solid gray;
  text-align: center;
  position: relative;
}
.child{        
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  width: 50%;
  height: 30%;
  margin: auto;
}
```

## More questions see: https://www.thatjsdude.com/interview/css.html
