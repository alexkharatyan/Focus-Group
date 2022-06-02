# CSS custom properties (variables)

Custom properties (sometimes referred to as CSS variables or cascading variables) are entities defined by CSS authors that contain specific values to be reused throughout a document. They are set using custom property notation (e.g., **--main-color: black;**) and are accessed using the **var()** function (e.g., **color: var(--main-color)**;).

Complex websites have very large amounts of CSS, often with a lot of repeated values. For example, the same color might be used in hundreds of different places, requiring global search and replace if that color needs to change. Custom properties allow a value to be stored in one place, then referenced in multiple other places. An additional benefit is semantic identifiers. For example, **--main-text-color** is easier to understand than **#00ff00**, especially if this same color is also used in other contexts.

Custom properties are subject to the cascade and inherit their value from their parent.

# Basic usage
Declaring a custom property is done using a custom property name that begins with a double hyphen (--), and a property value that can be any valid CSS value. Like any other property, this is written inside a ruleset, like so:

```css
element {
  --main-bg-color: brown;
}
```
Note that the selector given to the ruleset defines the scope that the custom property can be used in. A common best practice is to define custom properties on the **[:root](https://developer.mozilla.org/en-US/docs/Web/CSS/:root)** pseudo-class, so that it can be applied globally across your HTML document:
```css
:root {
  --main-bg-color: brown;
}
```

However, this doesn't always have to be the case: you maybe have a good reason for limiting the scope of your custom properties.
As mentioned earlier, you use the custom property value by specifying your custom property name inside the var() function, in place of a regular property value:
```css
element {
  background-color: var(--main-bg-color);
}
```

# Using the :root pseudo-class

Notice the repetitive CSS in the example above. The background color is set to brown in several places. For some CSS declarations, it is possible to declare this higher in the cascade and let CSS inheritance solve this problem naturally. For non-trivial projects, this is not always possible. By declaring a custom property on the :root pseudo-class and using it where needed throughout the document, a CSS author can reduce the need for repetition:
```css
:root {
  --main-bg-color: brown;
}

.one {
  color: white;
  background-color: var(--main-bg-color);
  margin: 10px;
  width: 50px;
  height: 50px;
  display: inline-block;
}
.four {
  color: white;
  background-color: var(--main-bg-color);
  margin: 10px;
  width: 100px;
}

.five {
  background-color: var(--main-bg-color);
}
```
Copy to Clipboard
This leads to the same result as the previous example, yet allows for one canonical declaration of the desired property value; very useful if you want to change the value across the entire page later.

# Inheritance of custom properties
Custom properties do inherit. This means that if no value is set for a custom property on a given element, the value of its parent is used. Take this HTML:
```css
<div class="one">
  <div class="two">
    <div class="three"></div>
    <div class="four"></div>
  </div>
</div>
```
... with the following CSS:
```css
.two {
  --test: 10px;
}

.three {
  --test: 2em;
}
```
In this case, the results of var(--test) are:

- For the class="two" element: 10px
- For the class="three" element: 2em
- For the class="four" element: 10px (inherited from its parent)
- For the class="one" element: invalid value, which is the default value of any custom property

Keep in mind that these are custom properties, not actual variables like you might find in other programming languages. The value is computed where it is needed, not stored for use in other rules. For instance, you cannot set a property for an element and expect to retrieve it in a sibling's descendant's rule. The property is only set for the matching selector and its descendants, like any normal CSS.

# Custom property fallback values

Using the var() function, you can define multiple fallback values when the given variable is not yet defined; this can be useful when working with Custom Elements and Shadow DOM.

Note: Fallback values aren't used to fix the browser compatibility. If the browser doesn't support CSS custom properties, the fallback value won't help. It's just a backup for the browser which supports CSS custom properties to choose a different value if the given variable isn't defined or has an invalid value.

The first argument to the function is the name of the custom property to be substituted. The second argument to the function, if provided, is a fallback value, which is used as the substitution value when the referenced custom property is invalid. The function only accepts two parameters, assigning everything following the first comma as the second parameter. If that second parameter is invalid, such as if a comma-separated list is provided, the fallback will fail. For example:
```css
.two {
  /* Red if --my-var is not defined */
  color: var(--my-var, red);
}

.three {
  /* pink if --my-var and --my-background are not defined */
  background-color: var(--my-var, var(--my-background, pink));
}

.three {
   /* Invalid: "--my-background, pink" */
  background-color: var(--my-var, --my-background, pink);
}
```
Including a custom property as a fallback, as seen in the second example above, is the correct way to provide more than one fallback. The technique has been seen to cause performance issues as it takes more time to parse through the variables.

# Handling invalid custom properties
Each CSS property can be assigned a defined set of values. If you try to assign a value to a property that is outside its set of valid values, it's considered invalid.

When the browser encounters an invalid value for a normal property, it discards the value, and elements are assigned the values that they would have had if the declaration simply did not exist.

However, when the values of custom properties are parsed, the browser doesn't yet know where they will be used, so it must consider nearly all values as valid.

Unfortunately, these valid values can be used, via the var() functional notation, in a context where they might not make sense. Properties and custom variables can lead to invalid CSS statements, leading to the new concept of valid at computed time.

When the browser encounters an invalid var() substitution, then the initial or inherited value of the property is used.

The next two examples illustrate this.

## Invalid normal properties

In this example we attempt to apply a value of 16px to the color property. Because this is invalid, the CSS is discarded and the result is as if the rule did not exist, so the previous color: blue rule is applied instead, and the paragraph is blue.
```HTML
HTML
<p>This paragraph is initially black.</p>
```
Copy to Clipboard
```css
CSS
p {
  color: blue;
}

p {
  color: 16px;
}
```

## Invalid custom properties
This example is just like the last one, except we use a custom property.

As expected, the browser substitutes the value of --text-color in place of var(--text-color), but 16px is not a valid property value for color. After substitution, the property doesn't make sense. The browser handles this situation in two steps:

Check if the property color is inheritable. It is, but this <p> doesn't have any parent with the color property set. So we move on to the next step.
Set the value to its default initial value, which is black.
```html
HTML
<p>This paragraph is initially black.</p>
```
```css
CSS
:root {
  --text-color: 16px;
}

p {
  color: blue;
}

p {
  color: var(--text-color);
}
```

# Values in JavaScript
To use the values of custom properties in JavaScript, it is just like standard properties.
```js
// get variable from inline style
element.style.getPropertyValue("--my-var");

// get variable from wherever
getComputedStyle(element).getPropertyValue("--my-var");

// set variable on inline style
element.style.setProperty("--my-var", jsVar + 4);
```

# [var()](https://developer.mozilla.org/en-US/docs/Web/CSS/var)

The var() CSS function can be used to insert the value of a custom property (sometimes called a "CSS variable") instead of any part of a value of another property.
The var() function cannot be used in property names, selectors or anything else besides property values. (Doing so usually produces invalid syntax, or else a value whose meaning has no connection to the variable.)

Syntax
The first argument to the function is the name of the custom property to be substituted. An optional second argument to the function serves as a fallback value. If the custom property referenced by the first argument is invalid, the function uses the second value.
```
var( <custom-property-name> , <declaration-value>? )
```

## Values
- custom-property-name
A custom property's name represented by an identifier that starts with two dashes. Custom properties are solely for use by authors and users; CSS will never give them a meaning beyond what is presented here.

- declaration-value
The custom property's fallback value, which is used in case the custom property is invalid in the used context. This value may contain any character except some characters with special meaning like newlines, unmatched closing brackets, i.e. ), ], or }, top-level semicolons, or exclamation marks.

## Custom properties with fallbacks for use when the property has not been set
```css
/* Fallback */
/* In the component's style: */
.component .header {
  color: var(--header-color, blue); /* header-color isn't set, and so remains blue, the fallback value */
}

.component .text {
  color: var(--text-color, black);
}

/* In the larger application's style: */
.component {
  --text-color: #080;
}
```
# What is the difference between CSS variables and preprocessor variables?
  
Variables are one of the major reasons CSS preprocessors exist at all. The ability to set a variable for something like a color, use that variable throughout the CSS you write, and know that it will be consistent, DRY, and easy to change is useful. You can use native CSS variables (“CSS Custom Properties”) for the same reasons. But there are also some important differences that should be made clear.


A simple example of preprocessor variable usage is like this:
```scss
$brandColor: #F06D06;

.main-header {
  color: $brandColor;
}
.main-footer {
  background-color: $brandColor;
}
  ```
  
That was the SCSS variant of Sass, but all CSS preprocessors offer the concept of variables: Stylus, Less, PostCSS, etc.

The above code would do nothing in a browser. The browser wouldn’t understand the declarations and toss them out. Preprocessors need to compile into CSS to be used. This code would compile to:
```css
.main-header {
  color: #F06D06;
}
.main-footer {
  background-color: #F06D06;
}
  ```
  
This is now valid CSS. The variable was part of the preprocessor language, not CSS itself. Once the code compiles, the variables are gone.

More recently, native CSS has started supporting CSS variables, or “CSS Custom Properties”. It allows you to work with variables directly in CSS. There is no compiling.

A simple example of CSS custom property usage is like this:
  ```css
:root {
  --main-color: #F06D06;
}

.main-header {
  color: var(--main-color);
}
.main-footer {
  background-color: var(--main-color);
}
  ```
  
These two demos achieve the exact same thing. We were able to define a color once and use it twice.

So then… why use one over another?

## Why would you use native CSS custom properties?
  
You can use them without the need of a preprocessor.
They cascade. You can set a variable inside any selector to set or override its current value.
When their values change (e.g. media query or other state), the browser repaints as needed.
You can access and manipulate them in JavaScript.
  
Regarding cascade, here’s a simple example of that:

 ```css
:root {
  --color: red;
}
body {
  --color: orange;
}
h2 {
  color: var(--color);
}
  ```
  
Any h2 will be orange, because any h2 will be a child of body, which has a higher applicable specificity.

You could even re-set variables within media queries and have those new values cascade through everywhere using them, something that just isn’t possible with preprocessor variables.

Check out [this example](https://codepen.io/chriscoyier/pen/ORdLvq?editors=0110) where a media query changes the variables which are used to set up a very simple grid:

  # Browser support of CSS Custom Properties

<img width="882" alt="Screen Shot 2022-06-02 at 02 30 13" src="https://user-images.githubusercontent.com/37399356/171512388-578c7f59-9beb-44b8-9bfc-3e5c237aa84d.png">
  
  ### Here is an examples of theme changeing
  - [https://codepen.io/michellebarker/pen/GzzrGJ](https://codepen.io/michellebarker/pen/GzzrGJ)
  - [https://developer.mozilla.org/en-US/docs/Web/CSS/var](https://developer.mozilla.org/en-US/docs/Web/CSS/var)
  
  # @supports
If you would like to write conditional CSS for when a browser supports custom properties or not:

@supports (--custom: property) {
  /* Isolated CSS for browsers that DOES support custom properties, assuming it DOES support @supports */
}

@supports not (--custom: property) {
  /* Isolated CSS for browsers that DON'T support custom properties, assuming it DOES support @supports */
}

  -------------------------------------------
  
  # CSS Functions
  [CSS Functions List](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions#transform_functions)
  [CSS Functions](https://css-tricks.com/complete-guide-to-css-functions/)
  
  Like any other programming language, CSS has functions. They can be inserted where you’d place a value, or in some cases, accompanying another value declaration. Some CSS functions even let you nest other functions within them!
  
  
 ## Basics of CSS Functions

  ![Image](https://i2.wp.com/css-tricks.com/wp-content/uploads/2020/04/LV2OI0TM.png?fit=1024%2C333&ssl=1)
  
  Unlike other programming languages, we cannot create our own functions in CSS, per se. That kind of logic is reserved for CSS selectors, which allow you to create powerful conditional styling rules. 
  
  ## Common CSS Functions
  
  - url()
  ```css
  .el {
    background: url(/images/image.jpg);
    }
 ```
    
  - attr()
  ```css
  /* <div data-example="foo"> */
div {
  content: attr(data-example);
}
```

  - calc()
  ```css
  .el {
  width: calc(100vw - 80px);
}
```

  - [lang()](https://codepen.io/ericwbailey/pen/XQNEYM)
```css
  p:lang(en) {
  quotes: "\201C" "\201D" "\2018" "\2019" "\201C" "\201D" "\2018" "\2019";
}
  ```
  
  - :not()
  ```css
  h3:not(:first-child) {
  margin-top: 0;
}
  ```
  
  ### CSS Custom Properties

  - Color Functions
  
  ```css
  .el {
  color: rgb(255, 0, 0);
  color: rgba(255, 0, 0, 0.5);
  color: rgb(255 0 0 / 0.5);
}
  ```
  
  - hsl() and hsla()
  ```css
  .el {
  background: hsl(100, 100%, 50%);
  background: hsla(100, 100%, 50%, 0.5);
  background: hsl(100 100% 50% / 0.5);
}
  ```
  
  ### Pseudo Class Selector Functions

  - :nth-child()
  - :nth-last-child()
  - :nth-of-type()
  - :nth-last-of-type()

  ### Animation Functions
  
  - cubic-bezier()
  - path()
  - steps()
  ```css
.el {
  animation: 2s infinite alternate steps(10);
}
  ```
This relatively new function allows you to set the easing timing across an animation, which allows for a greater degree of control over what part of the animation occurs when. Dan Wilson has another excellent writeup of how it fits into the existing animation easing landscape. 

  ### Sizing & Scaling (Transform) Functions
  - scaleX(), scaleY(), scaleZ(), scale3d(), and scale()
  - translateX(), translateY(), translateZ(), translate3d(), and translate()
  - perspective()
  - rotateX(), rotateY(), rotateZ(), rotate3d(), and rotate()
  - skewX(), skewY(), and skew()

  ### Filter Functions

  - brightness()
  - blur()
  - contrast()
  - grayscale()
  - invert()
  - opacity()
  - saturate()
  - sepia()
  - drop-shadow()
  - hue-rotate()
  - SVG filters 

  ### Comparison Functions
  - [clamp()](https://codepen.io/paigen11/pen/ExgGGMW)
  - max() and min()

  ### Logical Combinations
  - :is() and :where()
  
  ### Gradient Functions

  - linear-gradient() and repeating-linear-gradient()
  - radial-gradient() and repeating-radial-gradient()
  - conic-gradient() and repeating-conical-gradient

  ### Grid Functions

  - fit-content()
  - minmax()
  - repeat()
  
  ### Shape Functions

  - circle()
  - ellipse()
  - polygon()
  - inset()
  
  ### Miscellaneous Functions

  - element()
  - image-set()
  ```css
.responsive-background {
  background-image: 
    image-set("image.png" 1x,
              "image-2x.png" 2x,
              "image-print.png" 600dpi
    );
}
  ```
This function allows you to specify a list of images for the browser to select for a background image, based on what it knows about the capabilities of its display and its connection speed. It is analogous to what you would do with the srcset property.

  - ::slotted()
  ```css
::slotted(.marker) {
  background: lightyellow;
}
  ```
This is a pseudo-element selector used to target elements that have been placed into a slot inside a HTML template. ::slotted() is intended to be used when working with Web Components, which are custom, developer-defined HTML elements.
  
  Also a lot of depricated))
  
  # Why so many?
  
CSS is maligned as frequently as it is misunderstood. The guiding thought to understanding why all these functions are made available to us is knowing that CSS isn’t prescriptive — not every website has to look like a Microsoft Word document. 

The technologies that power the web are designed in such a way that someone with enough interest can build whatever they want. It’s a powerful, revolutionary concept, a large part of why the web became so ubiquitous.
  

