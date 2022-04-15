# Flexbox
#
##### The Flexbox Layout (Flexible Box) module (a [W3C Candidate Recommendation as of October 2017](https://www.w3.org/TR/css-flexbox/)) aims at providing a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic (thus the word “flex”).
#
##### Note: Flexbox layout is most appropriate to the components of an application, and small-scale layouts, while the Grid layout is intended for larger scale layouts.
#
###  Specification Status and Browser Support
##### The Flexbox specification has been a work in progress for over 3 years. Various browsers have implemented different versions experimentally. In September 2012, the 3rd major revision of the Flexbox syntax reached the W3C Candidate Recommendation stage. This means that the W3C is satisfied with the current syntax and is encouraging browser vendors to implement it.
#
##### Flexbox Specification Timeline:
- ##### July 2009 Working Draft (display: box;)
- ##### March 2011 Working Draft (display: flexbox;)
- ##### November 2011 Working Draft (display: flexbox;)
- ##### March 2012 Working Draft (display: flexbox;)
- ##### June 2012 Working Draft (display: flex;)
- ##### September 2012 Candidate Recommendation (display: flex;)

##### Browsers are adopting Flexbox quickly. Chrome 22+, Opera 12.1+, and Opera Mobile 12.1+ already support Flexbox as described in this article. Firefox 18 and Blackberry 10 will follow soon. I recommend reading this article in a supported browser to see working examples.
# The flex container
##### An area of a document laid out using flexbox is called a flex container. To create a flex container, we set the value of the area's container's display property to flex or inline-flex. As soon as we do this the direct children of that container become flex items. As with all properties in CSS, some initial values are defined, so when creating a flex container all of the contained flex items will behave in the following way.
- ##### Items display in a row (the flex-direction property's default is row).
- ##### The items start from the start edge of the main axis.
- ##### The items do not stretch on the main dimension, but can shrink.
- ##### The items will stretch to fill the size of the cross axis.
- ##### The flex-basis property is set to auto.
- ##### The flex-wrap property is set to nowrap.

##### The result of this is that your items will all line up in a row, using the size of the content as their size in the main axis. If there are more items than can fit in the container, they will not wrap but will instead overflow. If some items are taller than others, all items will stretch along the cross axis to fill its full size.
#
###### We’ll explore what they do, how you can use them, and what their results will actually look like.
## Display: Flex
##### Here’s our example webpage:
![](https://cdn-media-1.freecodecamp.org/images/ChnkgUaWEN6dmtS4EQCG60uqIjZVphsErq91)
##### You have four colored divs of various sizes, held within a grey container div. As of now, each div has defaulted to display: block. Each square thus takes up the full width of its line.
#
##### In order to get started with Flexbox, you need to make your container into a flex container. This is as easy as:
#
```
#container {  display: flex;}
```
#
![](https://cdn-media-1.freecodecamp.org/images/6WwoIEc45lUHUcFQCmD8GmziiISm2lO64Y1-)
##### Not a lot has changed — your divs are displayed inline now, but that’s about it. But behind the scenes, you’ve done something powerful. You gave your squares something called a flex context.
#
##### You can now start to position them within that context, with far less difficulty than traditional CSS.
#
# 1. Flex Direction
##### A Flexbox container has two axes: a main axis and a cross axis, which default to looking like this:
#
![](https://cdn-media-1.freecodecamp.org/images/HHwxqz2N4bNksz9YwcMBAtD0z9TTCxeNXNBS)
#
##### By default, items are arranged along the main axis, from left to right. This is why your squares defaulted to a horizontal line once you applied display: flex.
#
##### Flex-direction, however, let’s you rotate the main axis.
#
```
#container {  display: flex;  flex-direction: column;}
```
#
##### There’s an important distinction to make here: flex-direction: column doesn’t align the squares on the cross axis instead of the main axis. It makes the main axis itself go from horizontal to vertical.
#
##### There are a couple of other options for flex-direction, as well: row-reverse and column-reverse.
#
![](https://cdn-media-1.freecodecamp.org/images/zYdQGSmhtMyqcAbEUDoEehohC8E-gtgvQx6b)
#
# 2. Justify Content
##### Justify-content controls how you align items on the main axis.
#
##### Here, you’ll dive a bit deeper into the main/cross axis distinction. First, let’s go back to flex-direction: row.
#
```
#container {  display: flex;  flex-direction: row;  justify-content: flex-start;}
```
#
##### You have five commands at your disposal to use justify-content:
#
- #### Flex-start
- #### Flex-end
- #### Center
- #### Space-between
- #### Space-around
- #### space-evenly

![](https://cdn-media-1.freecodecamp.org/images/OBGVr-DdHiQ2y9VOWuhXqXeGnFnyDSBTx7hv)
#
##### Space-around and space-between are the least intuitive. Space-between gives equal space between each square, but not between it and the container.
#
##### Space-around puts an equal cushion of space on either side of the square — which means the space between the outermost squares and the container is half as much as the space between two squares (each square contributing a non-overlapping equal amount of margin, thus doubling the space).
#
##### A final note: remember that justify-content works along the main-axis, and flex-direction switches the main-axis. This will be important as you move to…
#
# 3. Align Items
##### If you ‘get’ justify-content, align-items will be a breeze.
#
##### As justify-content works along the main axis, align-items applies to the cross axis.
#
![](https://cdn-media-1.freecodecamp.org/images/RfGcYLbTwhd9dmqLV9-F3ocjBE8Dp4ejvYXv)
#
##### Let’s reset our flex-direction to row, so our axes look the same as the above image.
#
##### Then, let’s dive into the align-items commands.
#
- #### flex-start
- #### flex-end
- #### center
- #### stretch
- #### baseline

##### The first three are exactly the same as justify-content, so nothing too fancy here.
#
##### The next two are a bit different, however.
#
##### You have stretch, in which the items take up the entirety of the cross-axis, and baseline, in which the bottom of the paragraph tags are aligned.
#
![](https://cdn-media-1.freecodecamp.org/images/UgsULw0Kk49l-l1wSzeurYNJKCmcA-01oE8a)
#
##### (Note that for align-items: stretch, I had to set the height of the squares to auto. Otherwise the height property would override the stretch.)
#
##### For baseline, be aware that if you take away the paragraph tags, it aligns the bottom of the squares instead, like so:
#
![](https://cdn-media-1.freecodecamp.org/images/dIxrfoUa2r7vM62TGAlKN2KGOnIMmeNM-Gwr)
#
##### To demonstrate the main and cross axes better, let’s combine justify-content and align-items and see how centering works different for the two flex-direction commands:
#
![](https://cdn-media-1.freecodecamp.org/images/u9tCV-zRt3qpgSyNQt53e-eRz0-HIrsqqOk-)
#
##### With row, the squares are set up along a horizontal main axis. With column, they fall along a vertical main axis.
#
##### Even if the squares are centered both vertically and horizontally in both cases, the two are not interchangeable!

# 4. Align Self
##### Align-self allows you to manually manipulate the alignment of one particular element.
##### The align-self property of Flex Items effectively overrides the Flex Container’s align-items property for that item. It has the same possible values as align-items:
#
- #### stretch (default)
- #### lex-start
- #### flex-end
- #### center
- #### baseline

##### It’s basically overriding align-items for one square. All the properties are the same, though it defaults to auto, in which it follows the align-items of the container.
#
```
#container {  align-items: flex-start;}
```
#
```
.square#one {  align-self: center;}// Only this square will be centered.
```
#
##### Let’s see what this looks like. You’ll apply align-self to two squares, and for the rest apply align-items: center and flex-direction: row.
![](https://cdn-media-1.freecodecamp.org/images/HbnMZT330ylw5idocqrjOfp9DrlZt9JrJm9o)
# 6. [Align-content](https://developer.mozilla.org/en-US/docs/Web/CSS/align-content)
##### This aligns a flex container’s lines within when there is extra space in the cross-axis, similar to how justify-content aligns individual items within the main-axis.
##### Note: This property only takes effect on multi-line flexible containers, where flex-wrap is set to either wrap or wrap-reverse). A single-line flexible container (i.e. where flex-wrap is set to its default value, no-wrap) will not reflect align-content.
- #### stretch (default)
- #### flex-start
- #### flex-end
- #### center
- #### space-between
- #### space-around

# 7. Flex-wrap
##### Up until now, every Flex Container has had only one Flex Line. Using flex-wrap you can create Flex Containers with multiple Flex Lines. The possible values for flex-wrap are:
- #### nowrap (default)
- #### wrap
- #### wrap-reverse

##### If flex-wrap is set to wrap, Flex Items wrap onto additional Flex Lines if there is not enough room for them on one Flex Line. Additional Flex Lines are added in the direction of the Cross Axis.
#
# 8. Flex-flow
##### flex-flow is a shorthand for flex-direction and flex-wrap.
#
```
.flex-container {
  -webkit-flex-flow: column nowrap;
  flex-flow: column nowrap;
}
```
#
# 13. Flex-basis
![](https://media.tproger.ru/uploads/2017/02/flex_10.gif)
##### flex-basis affects the size of elements along the main axis. Let's see what happens if we change the direction of the main axis:
![](https://media.tproger.ru/uploads/2017/02/770x284_flex-11.gif)
##### Note that we also had to change the height of the elements: flex-basis can determine both the height of the elements and their width depending on the direction of the axis.
##### If set to 0, the extra space around content isn’t factored in. If set to auto, the extra space is distributed based on its flex-grow value. [See this graphic](https://www.w3.org/TR/css-flexbox-1/images/rel-vs-abs-flex.svg).
#
# 11. Flex-grow
##### This defines the ability for a flex item to grow if necessary. It accepts a unitless value that serves as a proportion. It dictates what amount of the available space inside the flex container the item should take up.
##### If all items have flex-grow set to 1, the remaining space in the container will be distributed equally to all children. If one of the children has a value of 2, that child would take up twice as much of the space either one of the others (or it will try, at least).
#
##### For example we have divs with 120px width.
![](https://media.tproger.ru/uploads/2017/02/flex_pic_1.png)
##### If we set flex-grow: 1, all the divs will take the available equal space.
![](https://media.tproger.ru/uploads/2017/02/flex_pic_2.png)
##### Lets set to 999;
![](https://media.tproger.ru/uploads/2017/02/flex_pic_3.png)
##### And… nothing happened. This happened because flex-grow does not take absolute values, but relative ones. This means that it doesn't matter what value flex-grow has, what matters is how it relates to other blocks:
![](https://media.tproger.ru/uploads/2017/02/770x179_flex_12.gif)
##### Initially, the flex-grow of each block is 1, for a total of 6. This means that our container is divided into 6 parts. Each block will take up 1/6 of the available space in the container. When the flex-grow of the third block becomes 2, the container is divided into 7 parts: 1 + 1 + 2 + 1 + 1 + 1. Now the third block takes up 2/7 of the space, the rest - 1/7 each. Etc.
##### Flex-grow only works for the main axis until we change its direction.
#
# 12. Flex-shrink
##### The exact opposite of flex-grow. Specifies how much the block can be reduced in size. flex-shrink is used when the elements don't fit in the container. You define which elements should be reduced in size and which should not. By default, the flex-shrink value for each block is 1, which means that the blocks will shrink when the container shrinks.
##### Set flex-grow and flex-shrink to 1:
#
![](https://media.tproger.ru/uploads/2017/02/600x134_flex_13.gif)
##### Now let's change the flex-shrink value for the third block to 0. It has been prevented from shrinking, so its width will remain at 120px:
![](https://media.tproger.ru/uploads/2017/02/600x134_flex_14.gif)
##### flex-shrink is based on proportions. That is, if the first block has flex-shrink equal to 6, and the rest have it equal to 2, then this means that the first block will shrink three times faster than the rest.
#
# 14. flex
##### Replaces flex-grow, flex-shrink and flex-basis. Default values: 0 (grow) 1 (shrink) auto (basis).
#
##### Let's create two blocks:
#
```
.square#one {
  flex: 2 1 300px;
}
.square#two {
  flex: 1 2 300px;
}
```
#
##### Both have the same flex-basis. This means both will be 300px wide (container width: 600px plus margin and padding). But when the container starts to grow in size, the first box (with the larger flex-grow) will grow twice as fast, and the second box (with the largest flex-shrink) will shrink twice as fast:
![](https://media.tproger.ru/uploads/2017/02/flex_15.gif)
# 9. Margin
##### You may be familiar with the normal effect of margin: auto;. In Flexbox it does the same sort of thing, but it’s even more powerful. An “auto” margin will absorb extra space. It can be used to push Flex Items into different positions.

![](https://samanthaming.gumlet.io/flexbox30/31-flexbox-with-auto-margins.jpg.gz)
# 10. Order
##### Order is the simplest one. Setting orders for Flex Items adjusts their order when rendered. In this example, we set the order of one Flex Item to -1, causing it to be displayed before any other Flex Items.
![](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Ordering_Flex_Items/order-property.png)
## [Order example](https://developer.mozilla.org/en-US/docs/Web/CSS/order)
#
#
# 14. gap, row-gap, column-gap
##### The gap property explicitly controls the space between flex items. It applies that spacing only between items not on the outer edges.
#
```
.container {
  display: flex;
  ...
  gap: 10px;
  gap: 10px 20px; /* row-gap column gap */
  row-gap: 10px;
  column-gap: 20px;
}
```
##### It is not exclusively for flexbox, gap works in grid and multi-column layout as well.
#
# [Visibility](https://www.w3.org/TR/css-flexbox-1/#visibility-collapse)
##### When it is implemented, visibility: collapse; will be distinct from visibility: hidden; and display: none; for Flex Items. With collapse, the element will affect the Cross Size of the Flex Container, but it will not be displayed nor will it consume any space on the Main Axis. This will be useful for dynamically adding and removing Flex Items without affecting the Flex Container’s Cross Size.
##### Currently, visibility: collapse; does not appear to be correctly implemented in any browser. visibility: collapse; appears to do the same thing as visibility: hidden; in current implementations. I expect this to change soon.
# [The bugs and their workarounds](https://github.com/philipwalton/flexbugs)
##### Flexbox is certainly not without its bugs. The best collection of them I’ve seen is Philip Walton and Greg Whitworth’s Flexbugs. It’s an open-source place to track all of them, so I think it’s best to just link to that.
#
# Interesting Examples
#### [See more](https://css-tricks.com/snippets/css/a-guide-to-flexbox/#aa-flexbox-tricks)
#
## Conclusion
##### Even though we’ve just scratched the surface of Flexbox, these commands should be enough for you to handle most basic alignments — and to vertically align to your heart’s content.
#
#
[Sources](https://css-tricks.com/snippets/css/a-guide-to-flexbox/#aa-flexbox-tricks)


