# CSS Compilers
##### CSS preprocessors are scripting languages that extend the default capabilities of CSS. They enable us to use logic in our CSS code, such as variables, nesting, inheritance, mixins, functions, and mathematical operations. CSS preprocessors make it easy to automate repetitive tasks, reduce the number of errors and code bloat, create reusable code snippets, and ensure backward compatibility.
#
##### Each CSS preprocessor has its own syntax that they compile into regular CSS so that browsers can render it on the client side. Currently, the three most popular and stable CSS preprocessors are Sass, LESS, and Stylus, however there are many smaller ones as well. CSS preprocessors all do similar things but in a different way and with their own syntaxes. Each of them has some advanced features unique to them and their own ecosystem (tools, frameworks, libraries) as well.
#
## [Sass: Syntactically Awesome Style Sheet](https://sass-lang.com/)
##### Sass is the oldest CSS preprocessor, initially released in 2006. Its creators, Natalie Weizenbaum and Hampton Catlin were inspired by the Haml templating language which adds dynamic features to HTML. Their goal was to implement a similar dynamic functionality in CSS as well. So, they came up with a CSS preprocessor and named it Syntactically Awesome Style Sheets. Sass allows frontend developers to use variables, if/else statements, for/while/each loops, inheritance, and other computational logic in their CSS code.
#
##### Sass is written in Ruby, and originally it also needed Ruby to compile the code, which deterred many developers from using it. However, the introduction of the LibSass library gave a huge boost to the utilization of Sass. LibSass is a C/C++ library that allows us to parse Sass in other backend languages, for instance in Node, PHP, and even C.
#
#### Syntax
##### Sass has two syntaxes. The .sass file extension uses the older syntax that is indentation-based and omits semicolons and curly brackets from the code. The newer and more widely used syntax belonging to the .scss file extension. It uses the standard CSS syntax with braces and semicolons.
##### Below, you can see a basic example of the Sass/SCSS syntax. The code simply declares two variables, $primary-color and $primary-bg and applies them to the body HTML element.
#
```
/* SCSS */

$primary-color: seashell;
$primary-bg: darkslategrey;

body {
  color: $primary-color;
  background: $primary-bg;
}
```
##### The same code with the Sass syntax:
```
/* Sass */

$primary-color: seashell
$primary-bg: darkslategrey

body
  color: $primary-color
  background: $primary-bg
```
#
#### Features
##### In Sass, we can use variables to store values we want to reuse throughout the code. Sass variables are prepended with a $ sign, as you could see in the above example. Sass variables have scope so that we can use variables both locally and globally, which makes them quite versatile.
##### Sass follows the DRY (Don’t Repeat Yourself) programming principle in order to avoid duplication. It has two features that allow us to implement DRY: mixins and the @extend rule.
#
#### Tools & Examples
##### Sass has an incredible ecosystem with an active developer community and many tools and libraries. The two most widely-used frontend frameworks, [Bootstrap](https://getbootstrap.com/) and [Zurb Foundation](https://foundation.zurb.com/) are both written in Sass, which gives an extra traction to the language.
##### Moreover, Sass has powerful mixin libraries and authoring frameworks that further enhance the functionality of the language, such as [Compass](http://compass-style.org/) and [Bourbon](https://www.bourbon.io/). There are several notable companies who use Sass in their production sites, for instance Airbnb, Kickstarter, Hubspot, Zapier, Freshbooks, and many others.
#
#
# [LESS: Leaner Style Sheets](https://lesscss.org/#overview)
#
##### LESS was initially released three years after Sass, in 2009 by Alexis Sellier. It was influenced by Sass, therefore it implements many of its features such as mixins, variables, and nesting. Interestingly, later LESS also influenced Sass, as the newer SCSS syntax was inspired by the syntax of LESS.
#
##### The LESS CSS preprocessor is, in fact, a JavaScript library that extends the default functionalities of CSS. As it’s written in JavaScript, we need Node.js to install and run the LESS compiler. However, we can also compile LESS on the fly by adding .less files and the LESS converter to the <head> section of our HTML page.
#
#### Syntax
##### LESS uses the standard CSS syntax with the .less file extension. This means that a valid .css file is a valid .less file as well. Therefore, it’s really easy to pick up the syntax if you already know CSS, even if LESS has a few extra elements that you won’t find in CSS, such as the @ sign for variables.
##### For instance, the same example code we had a look in the Sass section above would look like this in LESS:
#
```
/* LESS */

@primary-color: seashell;
@primary-bg: darkslategrey;

body {
  color: @primary-color;
  background: @primary-bg;
}
```
##### Naturally, it compiles to the same CSS:
#
```
/* Compiled CSS */

body {
  color: seashell;
  background: darkslategrey;
}
```
#
#### Features
##### Just like Sass variables, LESS variables also have scopes which make them accessible where they are defined and called. Moreover, they cannot only be used within CSS rules but also inside selector and property names, URLs, and @import statements. For instance, we can store frequently used URL paths in variables and access them whenever we need to:
#
```
/* LESS */

@uploads: “../wp-content/uploads/”;
header {
  background-image: url(“@{uploads}/2018/03/bg-image.jpg);
}
```
##### This compiles to the following background rule:
```
/* Compiled CSS */

header {
  background-image: url("../wp-content/uploads/2018/03/bg-image.jpg");
}
```
##### In the example above, we can reuse the same @uploads variable several times and never have to worry again about getting the URL path wrong.
#
#### Tools and examples
##### Bootstrap’s decision to move Bootstrap 4 from LESS to Sass was a huge hit to the popularity of LESS, although it still has a LESS distribution. There are other LESS frameworks as well such as [Cardinal](http://cardinalcss.com/) and Semantic UI also has a LESS-only distribution.
#
##### LESS has some mixin libraries out there such as LESS Hat, however none of them are as powerful as Compass for Sass. There’s a great curated list of LESS tools on Github called Awesome LESS that’s worth having a look. We can also encounter LESS on production sites such as WeChat, Indiegogo, Transferwise, Patreon, Nordstrom, the Royal Opera House, and many others.
#
#
#### Stylus
##### The first version of Stylus was launched one year after LESS, in 2010 by TJ Holowaychuk, a former Node.js developer. Stylus is written in Node.js so that developers can easily integrate it into their Node projects. It was influenced by both Sass and LESS. Stylus combines the powerful logical abilities of Sass with the easy and straightforward setup of LESS.
#
#### Syntax
##### Developers frequently praise Stylus for its terse and flexible syntax. Stylus uses the .styl file extension and it allows us to write code in many different ways. We can use the standard CSS syntax, but we can also omit brackets, colons, and/or semicolons or leave out all punctuation altogether. For instance, our previous code example looks like this using the different syntaxes of Stylus:
#
```
/* Stylus standard CSS syntax */

primary-color = seashell;
primary-bg = darkslategrey;

body {
  color: primary-color;
  background: primary-bg;
}
```
##### However, we can remove the brackets:
#
```
/* Stylus syntax without brackets */

primary-color = seashell;
primary-bg = darkslategrey;

body
  color: primary-color;
  background: primary-bg;
```
##### Or, we can remove the brackets and the semicolons, too:
#
```
/* Stylus syntax without brackets and semicolons */

primary-color = seashell
primary-bg = darkslategrey

body
  color: primary-color
  background: primary-bg
```
##### Or, we can remove all punctuation (brackets, semicolons, colons):
#
```
/* Stylus syntax without punctuation */

primary-color = seashell
primary-bg = darkslategrey

body
  color primary-color
  background primary-bg
```
##### However, we can’t remove the assignment operator (=), as it indicates the declaration of a new variable. As Stylus is a pythonic (indentation-based) language, we always need to pay attention to proper indentation, otherwise the code won’t compile.
#
#### Tools & Examples
##### Stylus has a handful of mixin libraries such as [Nib](https://github.com/stylus/nib) and [Ride.css](https://github.com/ride-css/ride-css) that provide developers with ready-made cross-browser Stylus mixins. Although Stylus frameworks are not as famous as Bootstrap or Foundations, there are some good ones such as [Basis](https://getbasis.github.io/) and [Kouto Swiss](https://github.com/leny/kouto-swiss). The most notable corporate users of Stylus are Coursera, Livestorm, Accenture, Zenchef, HackerEarth, and a few others.
#
#
# [webpack](https://webpack.js.org/) vs [Gulp](https://gulpjs.com/) vs [Grunt](https://gruntjs.com/) vs [Browserify](https://browserify.org/)
##### (task managers)
#
### Why Use Tools Like Grunt, Gulp or webpack?
##### There are a lot of routine tasks that every front-end developer has to tackle. Of course, software builders tend to automate the workflow to save time. There are several operations that software engineers do every day.
#
![](https://d33wubrfki0l68.cloudfront.net/6c1711a2cb4ad76800852e5544ce8da84e0f51b1/fe476/images/tooling/webpack-gulp-grunt-browserify/m32zlnf.png)
#
##### As you can see, these tasks are not complicated but require much time and energy. With the help of workflow tools like Gulp, all these tasks can be automated.
#
![](https://d33wubrfki0l68.cloudfront.net/e79bc966ab44f426211a729b7949f373006bd476/20ceb/images/tooling/webpack-gulp-grunt-browserify/anyebzt.png)
#### Gulp vs Grunt: Speed
##### During development, Gulp’s creators have decided to utilize a completely different logic than Grunt. Gulp was created based on an asynchronous approach which gives an opportunity to process a lot of files independently. On the other hand, Grunt can run only one operation at a time.
#
##### TMWtech has done a test that compares the time required to compile a Sass file for both Gulp and Grunt. The results show us that Grunt had needed almost twice more time that Gulp (2.3 vs 1.3 sec). So, if speed is a vital factor then, of course, you need to choose Gulp. However, working on a small project, you won’t notice the difference.
#
##### If you work on a large project with a lot of tasks that need automation, it’s better speed-wise to use Gulp. In this case, the difference in time can influence your tooling decision.


# [webpack](https://webpack.js.org/)
##### webpack is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph from one or more entry points and then combines every module your project needs into one or more bundles, which are static assets to serve your content from.
#
##### webpack is increasingly popular because a lot of framework use webpack out of the box. There is a population of search queries for each of these automatic tools. As you can see, webpack was growing from 2015 to 2017. After April 2017, webpack became more widespread than Grunt and Gulp, so their popularity started to decrease.
![](https://d33wubrfki0l68.cloudfront.net/1f7a469dfd4f0851b2b6264092a21a95a17914db/c6442/images/tooling/webpack-gulp-grunt-browserify/osvuc0w.png)
