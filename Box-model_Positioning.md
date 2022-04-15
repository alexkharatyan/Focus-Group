# Positioning, the Box Model
There are ways to specify the visual layout of an HTML document
With positioning, the elusive "Flow" of CSS positioning comes into play. The flow in CSS is the logical way in which elements get placed on your screen.
#
##  [CSS Layout](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Introduction).
CSS page layout techniques allow us to take elements contained in a web page and control where they're positioned relative to the following factors: their default position in normal layout flow, the other elements around them, their parent container, and the main viewport/window. The page layout techniques we'll be covering in more detail in this module are:
- Normal flow
-  The [display](https://developer.mozilla.org/en-US/docs/Web/CSS/display) property (default flow)
-  Flexbox ([Flexible Box Layout CSS module](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout))
-  Grid (Grid Layout)
-  [Floats](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Floats) ([The line boxes](https://developer.mozilla.org/en-US/docs/Web/CSS/Visual_formatting_model#line_boxes))
- Positioning
- Table layout
- [Multiple-column](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Columns) layout (column-count)
#
# [The Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)
### History
Before HTML 4 and CSS, very few HTML elements supported both border and padding, so the definition of the width and height of an element was not very contentious. However, it varied depending on the element.
#
In 1996, CSS introduced margin, border and padding for many more elements. It adopted a definition width in relation to content, border, margin and padding similar to that for a table cell. This has since become known as the **W3C box model**.
#
Every element on a Web page, big, small, or in-between, is a **box**.
#
When a web page rendered, the browser's rendering engine represents each elements as a rectangular box.
![image](https://www.lilengine.co/sites/default/files/inline-images/Screen%20Shot%202019-04-14%20at%2023.59.07.png)
#
Every box is composed of four parts (or areas), defined by their respective edges.
[see here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model#content_area)
- ##### **Content area** — bounded by the content edge, contains the "real" content of the element, such as text, an image, or a video player. Its dimensions are the content width (or content-box width) and the content height (or content-box height). It often has a background color or background image.
- ##### **Padding area** — bounded by the padding edge, extends the content area to include the element's padding. Its dimensions are the padding-box width and the padding-box height.
- **Border area** — bounded by the border edge, extends the padding area to include the element's borders. Its dimensions are the border-box width and the border-box height.
- **Margin area** — bounded by the margin edge, extends the border area to include an empty area used to separate the element from its neighbors. Its dimensions are the margin-box width and the margin-box height.
When **margin collapsing** occurs, the margin area is not clearly defined since margins are shared between boxes.
[Margin collapsing](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)
The top and bottom margins of blocks are sometimes combined (collapsed) into a single margin whose size is the largest of the individual margins (or just one of them, if they are equal), a behavior known as margin collapsing. Note that the margins of floating and absolutely positioned elements never collapse.
There are other situations where elements do not have their margins collapsed:
- floated elements
- absolutely positioned elements
- inline-block elements
- elements with overflow set to anything other than visible (They do not collapse margins with their children.)
- cleared elements (They do not collapse their top margins with their parent block’s bottom margin.)
- the root element
w3c shows the following
![](https://www.w3.org/TR/CSS2/images/clearance.png)
#
Calculating the Widths and Heights of Boxes.
> **width of containing block (box)** = margin-left + border-left-width + padding-left + width + padding-right + border-right-width + margin-right
> **height of containing block (box)** = margin-top + border-top-width + padding-top + height + padding-bottom + border-bottom-width + margin-bottom
The box-sizing property can be used to adjust this behavior:
- **content-box** (called [The standard CSS box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model#the_standard_css_box_model)) gives you the default CSS box-sizing behavior. If you set an element's width to 100 pixels, then the element's content box will be 100 pixels wide, and the width of any border or padding will be added to the final rendered width, making the element wider than 100px.
- **border-box** (called [alternative CSS box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model#the_alternative_css_box_model)) tells the browser to account for any border and padding in the values you specify for an element's width and height This typically makes it much easier to size elements. box-sizing: border-box is the default styling that browsers use for the **`table`, `select`, and `button` elements, and for `input` elements whose type is radio, checkbox, reset, button, submit, color, or search**.
- **padding-box** - deprecated!!! (no support)


[Example](https://developer.mozilla.org/ru/docs/Web/CSS/box-sizing)
- ![](https://res.cloudinary.com/practicaldev/image/fetch/s--DHKBIxoD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lmi6ase1gdezqbtnlb5j.jpg)

Older versions of Internet Explorer, including IE6 (without a proper doctype) have a box model bug and calculate the width property inaccurately.
Width should only refer to the width of the content area. Older versions of IE and IE6 in quirks mode calculate the width as being the width of the content area + left and right paddings + the width of the right and left borders
Similarly it includes paddings and borders when calculating the height property.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/W3C_and_Internet_Explorer_box_models.svg/640px-W3C_and_Internet_Explorer_box_models.svg.png)

[There are two main types of boxes, block and inline](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model#block_and_inline_boxes).
In CSS we broadly have two types of boxes — **block boxes** and **inline boxes**.
Boxes also have an  **inner display type** and an  **outer display type**

If a box has an outer display type of block, it will behave in the following ways:
- The box will break onto a new line.
- The box will extend in the inline direction to fill the space available in its container. In most cases this means that the box will become as wide as its container, filling up 100% of the space available.
- The width and height properties are respected.
- Padding, margin and border will cause other elements to be pushed away from the box
Some HTML elements, such as `h1` and `p`, use block as their outer display type by default.
If a box has an outer display type of inline, then:
- The box will not break onto a new line.
- The width and height properties will not apply.
- Vertical padding, margins, and borders will apply but will not cause other inline boxes to move away from the box.
- Horizontal padding, margins, and borders will apply and will cause other inline boxes to move away from the box.
Some HTML elements, such as `a`, `span`, `em` and `strong` use inline as their outer display type by default.

### Aside: Inner and outer display types
Boxes also have an inner display type, however, which dictates how elements inside that box are laid out. By default, the elements inside a box are laid out in [normal flow](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Normal_Flow), which means that they behave just like any other block and inline elements (as explained above).
We can, however, change the inner display type by using display values like flex. If we set display: flex; on an element, the outer display type is block, but the inner display type is changed to flex.
#
# [The basics of positioning](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Positioning#test_your_skills!)
#
There are five different position values:
#
- Static Positioning - the default that every element gets
- position: relative - positioned element has taken its place in the normal flow, you can then modify its final position
- position: fixed - The viewport doesn't change when the window is scrolled, so a fixed positioned element will stay right where it is when the page is scrolled, creating an effect a bit like the old school "frames" days.
- position: absolute ([Layout and containing block](https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_block)) - element with position:absolute is removed from the document flow, which means the rest of the document acts as if the element weren’t there
- position: sticky - [examples](https://csslayout.io/sticky-header/)
  CSS position sticky has two main parts, sticky item & sticky container.
    - **Sticky Item** — is the element that we defined with the position: sticky styles. The element will float when the viewport position matches the position definition, for example: top: 0px .
    - **Sticky Containe**r —is the HTML element which wraps the sticky item. This is the maximum area that the sticky item can float in.

[examples ----> ](https://www.freecodecamp.org/news/learn-the-basics-the-css-position-property/)
#
Overlapping Elements (z-index) (show locally!!!)

Can you change the stacking order? Yes, you can, by using the z-index property. "z-index" is a reference to the z-axis.

Also works for flex box items
