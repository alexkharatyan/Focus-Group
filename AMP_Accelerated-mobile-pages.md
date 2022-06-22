# What’s AMP?
AMP stands for Accelerated Mobile Page. AMP is an open-source project, approved by Google which allows developers to build web pages that load faster on mobile devices. It improves the page-loading performance of web pages. Hence, you can get an outstanding and faster browsing experience on mobile devices.

The language of AMP is a stripped-down version of CSS and HTML that restricts the use of JavaScript.

AMPs are simple as it contains 10 times fewer data than a usual website or app. Therefore, it gives you informative content in the shortest possible time. It’s like you put your demand and the solution will be provided to you in a jiffy.

In recent times, AMP has been widely used for creating web pages that can load almost instantly. The open-source library is compatible across browsers and supports several platforms.

## Characteristics of AMP
- Offers instant delivery
- Enables developers to optimize delivery
- Open-source platform
- AMP pages do not support any types of forms
- AMP has improved discoverability due to carousel support
- Mandatory to declare height and width for images

## Advantages of AMP
- Fast Loading Speed: As per the research by Google, if a website takes more than three seconds to load, 40% of the users tend to leave that website. Several rules include the usage of just incline CSS and asynchronous JavaScript that is helpful in reducing the website loading speed. When a website loads faster, it helps to increase traffic and user engagement.

- Lower Bounce Rates: Having said earlier, loading time matters a lot in Google rankings. Hence, it will help in reducing bounce rates. Lower bounce rates are helpful for the search engine invalidating your pages.

- Improved SEO: With AMP, you will get improved SEO and keyword rankings in mobile devices. If a website takes time to load, it should affect SEO. Hence, faster loading speed will help the website rank higher in the Google search engine.

- Increased Ad views: With AMP, you can enhance the ability of images and banners. Hence, there will be a high ads view-ability rate and this helps in monetizing the website.

## Disadvantages of AMP
AMP is designed to load faster by showing only useful content with some visual limitations. These include:

- Cannot track user activity on AMP pages
- Not suitable for e-commerce websites as it doesn’t include fancy elements required to boost user engagement
- Unable to enhance search engine rankings
- Lazy load functionality for images
- Lower user engagement compared to HTML pages
- Concentrates only on speed by omitting other content
- May affect the page engagement

## When Should You Choose Accelerated Mobile Pages?
If you are an online publisher of news stories, blogs, and articles, then you should choose Accelerated Mobile Pages as they are preferred by mobile search results on Google.


# How AMP works
The following optimizations combined are the reason AMP pages are so fast they appear to load instantly:

### Execute all AMP JavaScript asynchronously
JavaScript is powerful, it can modify just about every aspect of the page, but it can also block DOM construction and delay page rendering. To keep JavaScript from delaying page rendering, AMP allows only asynchronous JavaScript.

AMP components may have JavaScript under the hood, but they’re carefully designed to make sure they don’t cause performance degradation.

While custom JS is allowed in amp-script, and third-party JS is allowed in iframes, it cannot block rendering. For example, if third-party JS uses the super-bad-for-performance document.write API, it does not block rendering the main page.

### Size all resources statically
External resources such as images, ads or iframes must state their size in the HTML so that AMP can determine each element’s size and position before resources are downloaded. AMP loads the layout of the page without waiting for any resources to download.

AMP uncouples document layout from resource layout. Only one HTTP request is needed to layout the entire doc (+fonts). Since AMP is optimized to avoid expensive style recalculations and layouts in the browser, there won’t be any re-layout when resources load.

### Don’t let extension mechanisms block rendering
AMP doesn’t let extension mechanisms block page rendering. AMP supports extensions for things like lightboxes, instagram embeds, tweets, etc. While these require additional HTTP requests, those requests do not block page layout and rendering.

Any page that uses a custom script must tell the AMP system that it will eventually have a custom tag. For example, the amp-iframe script tells the system that there will be an amp-iframe tag. AMP creates the iframe box before it even knows what it will include:

```html
<script async custom-element="amp-iframe" src="https://cdn.ampproject.org/v0/amp-iframe-0.1.js"></script>
```

### Keep all third-party JavaScript out of the critical path
Third-party JS likes to use synchronous JS loading. They also like to document.write more sync scripts. For example, if you have five ads on your page, and each of them cause three synchronous loads, each with a 1 second latency connection, you’re in 15 seconds of load time just for JS loading.

AMP pages allow third-party JavaScript but only in sandboxed iframes. By restricting them to iframes, they can’t block the execution of the main page. Even if they trigger multiple style re-calculations, their tiny iframes have very little DOM.

The time it takes to do style-recalculations and layouts are restricted by DOM size, so the iframe recalculations are very fast compared to recalculating styles and layout for the page.

### All CSS must be inline and size-bound
CSS blocks all rendering, it blocks page load, and it tends to get bloated. In AMP HTML pages, only inline styles are allowed. This removes 1 or often more HTTP requests from the critical rendering path compared to most web pages.

Also, the inline style sheet has a maximum size of 50 kilobytes(while JS to 150KB). While this size is big enough for very sophisticated pages, it still requires the page author to practice good CSS hygiene.

### Font triggering must be efficient
Web fonts are super large, so web font optimization is crucial to performance. On a typical page that has a few sync scripts and a few external style sheets, the browser waits and waits to start downloading these huge fonts until all this happens.

The AMP system declares zero HTTP requests until fonts start downloading. This is only possible because all JS in AMP has the async attribute and only inline style sheets are allowed; there’s no HTTP requests blocking the browser from downloading fonts.

### Minimize style recalculations
Each time you measure something, it triggers style recalculations which are expensive because the browser has to layout the entire page. In AMP pages, all DOM reads happen first before all the writes. This ensures there’s the max of one recalc of styles per frame.

Learn more about impact of style and layout recalculations on rendering performance.

### Only run GPU-accelerated animations
The only way to have fast optimizations is to run them on the GPU. GPU knows about layers, it knows how to perform some things on these layers, it can move them, it can fade them, but it can’t update the page layout; it will hand that task over to the browser, and that’s not good.

The rules for animation-related CSS ensure that animations can be GPU-accelerated. Specifically, AMP only allows animating and transitioning on transform and opacity so that page layout isn’t required. Learn more about using transform and opacity for animation changes.

### Prioritize resource loading
AMP controls all resource downloads: it prioritizes resource loading, loading only what’s needed, and prefetches lazy-loaded resources.

When AMP downloads resources, it optimizes downloads so that the currently most important resources are downloaded first. Images and ads are only downloaded if they are likely to be seen by the user, above the fold, or if the user is likely to quickly scroll to them.

AMP also prefetches lazy-loaded resources. Resources are loaded as late as possible, but prefetched as early as possible. That way things load very fast but CPU is only used when resources are actually shown to users.

### Load pages in an instant
Whenever mobile search results include AMP pages, Google starts loading resources for these pages even before you visit them.

The new preconnect API is used heavily to ensure HTTP requests are as fast as possible when they are made. With this, a page can be rendered before the user explicitly states they’d like to navigate to it; the page might already be available by the time the user actually selects it, leading to instant loading.

While prerendering can be applied to all web content, it can also use up a lot of bandwidth and CPU. AMP is optimized to reduce both of these factors. Prerendering only downloads resources above the fold and prerendering doesn’t render things that might be expensive in terms of CPU.

When AMP documents get prerendered for instant loading, only resources above the fold are actually downloaded. When AMP documents get prerendered for instant loading, resources that might use a lot of CPU (like third-party iframes) do not get downloaded.





# What's the criticism of AMP
Since AMP was launched it has received a fair share of opposition, both on technical implementation and the implications of Google's control. If you feel like going down the rabbit hole, then here is one of many articles criticizing AMP, with links to other like-minded articles that themselves contain plenty of further links. If not, then I'm happy to supply you with a brief recap.

- **Technical limitations**
Initially, AMP pages didn't allow any third-party JS, had a buggy analytics connection, limited styles, no comments, no social sharing buttons, no navigation, no sidebar, and the list goes on. The resulting pages were quite spartan in appearance, reminiscent of early blog posts. As you can imagine, website owners weren't too happy about stripping their pages of all the features that made them special — it seemed too big a price to pay for an improvement in mobile speed.

- **Google control**
A much bigger issue, however, was taken with Google involvement. Since Google was effectively hosting AMP pages and serving them under its own domain, it looked like the search engine was appropriating both the content and the traffic of AMP websites. And then there was the preferential treatment of AMP pages in Google's search results, which didn't look good either.

- **AMP response**
As of today, most of the issues listed above have been addressed by the AMP team. The AMP catalog has added plenty of administrative and design components, including navigation, forms, and analytics. AMP pages are also no longer served via Google domain, and the team is working towards extending Google cache benefits to other fast pages.

The only thing that remains is the preferential treatment of newsy AMP pages that get featured in dedicated SERP panels. There are currently no plans to address this issue. On the contrary, it's likely to be magnified as AMP Stories gain momentum and also become featured in search results. Is it fair? Perhaps not, but then there are plenty of other rich snippets with varying degrees of fairness, so I wouldn't say that it's a uniquely AMP issue.


# What's the future of AMP
The AMP project is far from the fastest horse in Google's portfolio, but it looks like it's here to stay. There is a steady output of new features, the team has proven reliable in addressing developer concerns, and the project stats all look healthy. So, what's next for the AMP project?

- **AMP-only websites
High on the list of priorities, and well within reach, is using AMP to build fully functional websites. Three years ago AMP was incredibly limiting, only allowing for the most basic of pages. But the list of components kept growing, and there is hardly a feature now that can't be replicated using AMP.

To bridge the remaining gap, AMP has finally allowed the use of JavaScript, which was previously a big no-no. It is limited to 150KB, but it should be enough to implement those features that are not yet covered by AMP.

- **New content types
AMP Stories and AMP Email are in the early stages and haven't seen much use as of yet, but the team is fully behind those applications. AMP Stories is a storytelling format much like the one used by Snapchat, Instagram, and Facebook, while AMP Email is a next-generation email that's both dynamic and interactive — basically a webpage served via an email client.

- **AMP Bento
This is still a concept, but the goal is for AMP components to be used within non-AMP pages. The idea is to lower the entry barrier by allowing some of the AMP benefits without a full commitment to the AMP framework. But, regardless of whether it's an onboarding strategy or a genuine attempt at creating a faster web, higher flexibility is always welcome.

- **Non-AMP pre-rendering
It seems only fair that Google should extend the benefits of pre-rendering to those pages that are as fast as AMP pages. And the solution is in the works, but there are two big obstacles to overcome.

First, there is no reliable way to evaluate the perceived performance of a non-AMP page. With an AMP page, you have design restrictions that guarantee it's going to feel fast. And while there is a number of speed tests that can be used on non-AMP pages, none of them are an accurate reflection of how fast the page feels. There is no solution yet, but the AMP team is on it and it's likely to be a cross between Chrome UX report, Lighthouse, and AMP validator.

Second, pre-rendering poses a security risk, because it sends a fetch request for a page before there is an expressed intent to visit it, so there is an exchange of information without user consent. Google gets around this by hosting AMP pages on its server and using it as an information buffer. Luckily, the new Signed Exchange technology will allow Google to cache non-AMP pages as well, so this issue is all but solved.

## Should you implement AMP in 2021
I know you expect me to say that it depends, but it only depends on whether or not you are a news site. If yes, then you should have converted to AMP three years ago. But if you are not a news site and you are not after those headline panels, then I don't see a convincing case for converting to AMP in the near future.

The key benefit of AMP is page speed that comes from radical optimization and is further enhanced through Google cache. But similar speed can be achieved with regular mobile optimization, while Google cache is soon to be extended to non-AMP pages. So, if your website is already fast, then I would stay away from AMP as there is no added benefit of converting.

That being said, there is no longer an argument against AMP either. Back in the day, it used to cut your pages down to their most basic versions. Now, it has enough flexibility to build even the most advanced of pages. So, if your mobile website is slow and you are looking for a way to optimize it, then AMP is a perfectly valid option to consider.

Well, I guess it does depend after all.

## Final thoughts
The AMP project has reached the point where it offers impressive speed benefits without any usability sacrifices. But it's also on the brink of extending those benefits to fast non-AMP pages. So it's about to become **just another option** for mobile optimization.




