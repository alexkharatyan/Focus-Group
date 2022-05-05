# CSS Media Queries
Media queries can modify the appearance (and even behavior) or a website or app based on a matched set of conditions about the user’s device, browser or system settings.
CSS Media queries are a way to target browser by certain characteristics, features, and user preferences, then apply styles or run other code based on those things.

Perhaps the most common media queries in the world are those that target particular viewport ranges and apply custom styles, which birthed the whole idea of responsive design.
```Css
/* When the browser is at least 600px and above */
@media screen and (min-width: 600px) {
  .element {
    /* Apply some styles */
  }
}
```
There are lots of other things we can target beside viewport width. That might be screen resolution, device orientation, operating system preference, or even more among a whole bevy of things we can query and use to style content.

## Using media queries
Media queries are commonly associated with CSS, but they can be used in HTML and JavaScript as well.

- ### HTML
There are a few ways we can use media queries directly in HTML.

There’s the <link> element that goes right in the document <head>. In this example. we’re telling the browser that we want to use different stylesheets at different viewport sizes:
```Html
<html>
  <head>
    <!-- Served to all users -->
    <link rel="stylesheet" href="all.css" media="all" />
    <!-- Served to screens that are at least 20em wide -->
    <link rel="stylesheet" href="small.css" media="(min-width: 20em)" />
    <!-- Served to screens that are at least 64em wide -->
    <link rel="stylesheet" href="medium.css" media="(min-width: 64em)" />
    <!-- Served to screens that are at least 90em wide -->
    <link rel="stylesheet" href="large.css" media="(min-width: 90em)" />
    <!-- Served to screens that are at least 120em wide -->
    <link rel="stylesheet" href="extra-large.css" media="(min-width: 120em)" />
    <!-- Served to print media, like printers -->
    <link rel="stylesheet" href="print.css" media="print" />
  </head>
  <!-- ... -->
</html>
  ```
Why would you want to do that? It can be a nice way to fine-tune the performance of your site by splitting styles up in a way that they’re downloaded and served by the devices that need them.

But just to be clear, this doesn’t always prevent the stylesheets that don’t match those media queries from downloading, it just assigns them a low loading priority level.

So, if a small screen device like a phone visits the site, it will only download the stylesheets in the media queries that match its viewport size. But if a larger desktop screen comes along, it will download the entire bunch because it matches all of those queries (well, minus the print query in this specific example).

That’s just the <link> element. As our guide to responsive images explains, we can use media queries on <source> element, which informs the <picture> element what version of an image the browser should use from a set of image options.

  ```html
<picture>
  <!-- Use this image if the screen is at least 800px wide -->
  <source srcset="cat-landscape.png" media="(min-width: 800px)">
  <!-- Use this image if the screen is at least 600px wide -->
  <source srcset="cat-cropped.png" media="(min-width: 600px)">

  <!-- Use this image if nothing matches -->
  <img src="cat.png" alt="A calico cat with dark aviator sunglasses.">
</picture>
  ```
Again, this can be a nice performance win because we can serve smaller images to smaller devices — which presumably (but not always) will be low powered devices that might be limited to a data plan.

And let’s not forget that we can use media queries directly on the <style> element as well:
```css
<style>
  p {
    background-color: blue;
    color: white;
  }
</style>

<style media="all and (max-width: 500px)">
  p {
    background-color: yellow;
    color: blue;
  }
</style>
  ```
  
  - ### CSS
Again, CSS is the most common place to spot a media query in the wild. They go right in the stylesheet in an @media rule that wraps elements with conditions for when and where to apply a set of styles when a browser matches those conditions.
```css
/* Viewports between 320px and 480px wide */
@media only screen and (min-device-width: 320px) and (max-device-width: 480px) {
  .card {
    background: #bada55;
  }
}
  ```
It’s also possible to scope imported style sheet but as a general rule avoid using @import since it performs poorly.
```css
/* Avoid using @import if possible! */

/* Base styles for all screens */
@import url("style.css") screen;
/* Styles for screens in a portrait (narrow) orientation */
@import url('landscape.css') screen and (orientation: portrait);
/* Print styles */
@import url("print.css") print;
  ```
  
  - ### JavaScript
We can use media queries in JavaScript, too! And guess, what? They’re work a lot like they do in CSS. The difference? We start by using the window.matchMedia() method to define the conditions first.

So, say we want to log a message to the console when the browser is at least 768px wide. We can create a constant that calls matchMedia() and defines that screen width:
```js
// Create a media condition that targets viewports at least 768px wide
const mediaQuery = window.matchMedia( '( min-width: 768px )' )
Then we can fire log to the console when that condition is matched:

// Create a media condition that targets viewports at least 768px wide
const mediaQuery = window.matchMedia( '( min-width: 768px )' )
 
// Note the `matches` property
if ( mediaQuery.matches ) {
  console.log('Media Query Matched!')
}
  ```
Unfortunately, this only fires once so if the alert is dismissed, it won’t fire again if we change the screen width and try again without refreshing. That’s why it’s a good idea to use a listener that checks for updates.
```js
// Create a condition that targets viewports at least 768px wide
const mediaQuery = window.matchMedia('(min-width: 768px)')
 
function handleTabletChange(e) {
  // Check if the media query is true
  if (e.matches) {
    // Then log the following message to the console
    console.log('Media Query Matched!')
  }
}
 
// Register event listener
mediaQuery.addListener(handleTabletChange)

// Initial check
handleTabletChange(mediaQuery)
  ```
  
  ## Anatomy of a Media Query
  Now that we’ve seen several examples of where media queries can be used, let’s pick them apart and see what they’re actually doing.
  
  ![](https://i0.wp.com/css-tricks.com/wp-content/uploads/2020/09/media-query-anatomy.jpg?resize=1536%2C101&ssl=1)
  
  - #### @media
  
  ```css
@media [media-type] ([media-feature]) {
  /* Styles! */
}
  ```
  
The first ingredient in a media query recipe is the @media rule itself, which is one of many CSS at-rules. Why does @media get all the attention? Because it’s geared to the type of media that a site is viewed with, what features that media type supports, and operators that can be combined to mix and match simple and complex conditions alike.

- #### Media types
  
```css
    @media screen {
      /* Styles! */

    }
```
  
What type of media are we trying to target? In many (if not most) cases, you’ll see a screen value used here, which makes sense since many of the media types we’re trying to match are devices with screens attached to them.

But screens aren’t the only type of media we can target, of course. We have a few, including:

- all: Matches all devices
- print: Matches documents that are viewed in a print preview or any media that breaks the content up into pages intended to print.
- screen: Matches devices with a screen
- speech: Matches devices that read the content audibly, such as a screenreader. This replaces the now deprecated aural type since Media Queries Level 4.
  

- ## [Media features](https://developer.mozilla.org/en-US/docs/Web/CSS/@media#media_features)
Once we define the type of media we’re trying to match, we can start defining what features we are trying to match it to. We’ve looked at a lot of examples that match screens to width, where screen is the type and both min-width and max-width are features with specific values.

But there are many, many (many!) more “features” we can match. Media Queries Level 4 groups 18 media features into 5 categories.

- ### Viewport/Page Characteristics
  ![Viewport/Page Characteristics](/images/viewport-page-characteristics.png)
- ### Display Quality
![Display Quality](/images/display-quality.png)
- ### Color
![Color](images/color)
  - ### Interaction
![Interaction](/images/interaction.png)
   - ### Video Prefixed
  The spec references user agents, including TVs, that render video and graphics in two separate planes that each have their own characteristics. The following features describe those planes.
![Video Prefixed](/images/video-prefixed.png)
  - ### Scripting
![Scripting](/images/scripting.png)
   - ### User Preference
![User Preference](/images/user-preference.png)
 - ### Deprecated
![Deprecated](/images/deprecated.png)
  
  
- ## Operators
Media queries support logical operators like many programming languages so that we can match media types based on certain conditions. The @media rule is itself a logical operator that is basically stating that “if” the following types and features are matches, then do some stuff.

- ### and
But we can use the and operator if we want to target screens within a range of widths:
  
```css
/* Matches screen between 320px AND 768px */
@media screen (min-width: 320px) and (max-width: 768px) {
  .element {
    /* Styles! */
  }
}
  ```
  
- ### or (or comma-separated)
We can also comma-separate features as a way of using an or operator to match different ones:

  ```css
/* 
  Matches screens where either the user prefers dark mode or the screen is at least 1200px wide */
@media screen (prefers-color-scheme: dark), (min-width 1200px) {
  .element {
    /* Styles! */
  }
}
  ```
  
- ### [not](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#inverting_a_querys_meaning)
Perhaps we want to target devices by what they do not support or match. This declaration removes the body’s background color when the device is a printer and can only show one color.

```css
@media print and ( not(color) ) {
  body {
    background-color: none;
  }
}  
  ```
  
  ## Do you really need CSS media queries?
Media queries are a powerful tool in your CSS toolbox with exciting hidden gems. But if you accomodate your design to every possible situation you’ll end up with a codebase that’s too complex to maintain and, as we all know, CSS is like a bear cub: cute and inoffensive but when it grows it will eat you alive.

That’s why I recommend following Ranald Mace’s concept of Universal Design which is “the design of products to be usable by all people, to the greatest extent possible, without the need for adaptation or specialized design.” 
   talking about universal design on the web is hard and almost sound utopian, but think about it, there are around 150 different browsers, around 50 different combinations of user preferences, and as we mentioned before more than 24000 different and unique Android devices alone.

This means that there are at least 18 million possible cases in which your content might be displayed.
  That’s why assuming is really dangerous, so when you design, develop and think about your products leave assumptions behind and use media queries to make sure that your content is displayed correctly in any contact and before any user.
  
  ## Accessibility
Many of the features added in Media Queries Level 4 are centered around accessibility.
  
 ### prefers-reduced-motion
  
prefers-reduced-motion detects if the user has the reduced motion preference activated to minimize the amount of movements and animations. It takes two values:

- #### no-preference: Indicates that the user has made no preference known to the system.
- #### reduce: Indicates that user has notified the system that they prefer an interface that minimizes the amount of movement or animation, preferably to the point where all non-essential movement is removed.

![](https://i0.wp.com/css-tricks.com/wp-content/uploads/2020/09/macos-preference-motion.png?w=1560&ssl=1)
 
  This preference is generally used by people who suffer from vestibular disorder or vertigo, where different movements result in loss of balance, migraine, nausea or hearing loss. If you ever tried to spin quickly and got dizzy, you know what it feels like.

```css
  @media screen and (prefers-reduced-motion: reduce) {  
  * {
    /* Very short durations means JavaScript that relies on events still works */
    animation-duration: 0.001ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.001ms !important;
  }
}
  ```

Popular frameworks like Bootstrap have this feature on by default. In my opinion there is no excuse not to use prefers-reduced-motion — just use it. 
  
  ### prefers-contrast
The prefers-contrast feature informs whether the user has chosen to increase or reduce contrast in their system preferences or the browser settings. It takes three values:

- #### no-preference: When a user has made no preference known to the system. If you use it as a boolean it’ll evaluate false.
- #### high: When a user has selected the option to display a higher level of contrast.
- #### low: When a user has selected the option to display a lower level of contrast.
  
![](https://i0.wp.com/css-tricks.com/wp-content/uploads/2020/09/macos-preference-contrast.png?w=1560&ssl=1)
At the moment of writing this feature is not supported by any browser. Microsoft has done a non-standard earlier implementation with the -ms-high-contrast feature that works only on Microsoft Edge v18 or earlier (but not Chromium-based versions).

  ```css
.button {
  background-color: #0958d8;
  color: #fff;
}

@media (prefers-contrast: high) {
  .button {
    background-color: #0a0db7;
  }
}
  ```
  
This example is increasing the contrast of a the class button from AA to AAA when the user has high contrast on.
  
  ### inverted-colors
The inverted-colors feature informs whether the user has chosen to invert the colors on their system preferences or the browser settings. Sometimes this option is used as an alternative to high contrast. It takes three values:

- #### none: When colors are displayed normally
- #### inverted: When a user has selected the option to invert colors
  
![](https://i0.wp.com/css-tricks.com/wp-content/uploads/2020/09/macos-preference-invert-colors.png?w=1560&ssl=1)
The problem with inverted colors is that it’ll also invert the colors of images and videos, making them look like x-ray images. By using a CSS invert filter you can select all images and videos and invert them back.

  
```css
@media (inverted-colors) {
  img, video { 
    filter: invert(100%);
  }
}
  
```

At the time of writing this feature is only supported by Safari.

### prefers-color-scheme
Having a “dark mode” color scheme is something we’re seeing a lot more of these days, and thanks to the prefers-color-scheme feature, we can tap into a user’s system or browser preferences to determine whether we serve a “dark” or a “light” theme based on the ir preferences.

It takes two values:

- #### light: When a user has selected that they prefer a light theme or has no active preferences
- #### dark: When a user has selected a dark display in their settings
  ![](https://paper-attachments.dropbox.com/s_0BFBF55A2024DE950EFA25781444032C5BBE17E7EC9DD277E9E0361558E9B210_1595791834440_Screen+Shot+2020-07-26+at+4.28.13+PM.png)
 

```css

  body {
  --bg-color: white; 
  --text-color: black;

  background-color: var(--bg-color);
  color: var(--text-color);
}

@media screen and (prefers-color-scheme: dark) {
  body {
    --bg-color: black;
    --text-color: white;
  }
}
```

#
  
## What lies ahead?
[Media Queries Level 5](https://www.w3.org/TR/mediaqueries-5/) is currently in Working Draft status, which means a lot can change between now and when it becomes a recommendation. But it includes interesting features that are worth mentioning because they open up new ways to target screens and adapt designs to very specific conditions.

#### User preference media features
Hey, we just covered these in the last section! Oh well. These features are exciting because they’re informed by a user’s actual settings, whether they are from the user agent or even at the operating system level.

#### Detecting a forced color palette
This is neat. Some browsers will limit the number of available colors that can be used to render styles.
  This is called “forced colors mode” and, if enabled in the browser settings, the user can choose a limited set of colors to use on a page. As a result, the user is able to define color combinations and contrasts that make content more comfortable to read.

The forced-colors feature allows us to detect if a forced color palette is in use with the active value.If matched, the browser must provide the required color palette through the CSS system colors. The browser is also given the leeway to determine if the background color of the page is light or dark and, if appropriate, trigger the appropriate prefers-color-scheme value so we can adjust the page.

#### Detecting the maximum brightness, color depth, and contrast ratio
Some devices (and browsers) are capable of super bright displays, rendering a wide range of colors, and high contrast ratios between colors. We can detect those devices using the dynamic-range feature, where the high keyword matches these devices and standard matches everything else.

We’re likely to see changes to this because, as of right now, there’s still uncertainty about what measurements constitute “high” levels of brightness and contrast. The browser may get to make that determination.

#### Video prefixed features
The spec talks about some screens, like TVs, that are capable of displaying video and graphics on separate “planes” which might be a way of distinguishing the video frame from other elements on the screen. As such, Media Queries Level 5 is proposing a new set of media features aimed at detecting video characteristics, including color gamut and dynamic range.

There are also proposals to detect video height, width and resolution, but the jury’s still out on whether those are the right ways to address video.
  
  # [Examples](https://css-tricks.com/a-complete-guide-to-css-media-queries/#aa-examples)
  
