---
template: SinglePost
title: Lazyload Youtube Videos
status: Featured / Published
date: '2018-03-27'
featuredImage: 'https://res.cloudinary.com/practicaldev/image/fetch/s--ESjkTlur--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://i.imgur.com/IT0tvqp.png'
excerpt: >-
over 500KB that my users would have to download on top of the website, regardless if they'll watch the video. Do you have any idea how heavy this might hit your users, specially the ones with slow connection or low performing machines? To add insult to injury they'd also be being tracked—Hi Google—for just loading a video they didn't even know was there.
categories:
  - category: News
meta:
  canonicalLink: ''
  description: test meta description
  noindex: false
  title: test meta title
---

The code for embedding an YouTube video, as of August 2019, goes like this:

```html
<iframe 
  width="560" 
  height="315" 
  src="https://www.youtube.com/embed/Y8Wp3dafaMQ" 
  frameborder="0" 
  allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
  allowfullscreen>
</iframe>
```

So I thought what if instead of the actual video I showed just its cover linked to the video? It would still kinda look like an embedded video but it would require only a single image upfront. Thankfully YouTube has an URL schema for video thumbnails.

```
<a href="https://www.youtube.com/embed/Y8Wp3dafaMQ">
  <img src="https://i3.ytimg.com/vi/Y8Wp3dafaMQ/hqdefault.jpg">
</a>
```

Cool, but I really don't want to have to create a whole new page just for this teeny tiny snippet of code. Well, we're in luck cause <iframe> has just the perfect thing for us—the srcdoc attribute. With it you can source the <iframe> directly in the hosting page. Just beware that it won't work on Edge or IE and that we can't use double quotes.

```
<iframe 
  ...
  srcdoc="<a href=https://www.youtube.com/embed/Y8Wp3dafaMQ><img src=https://i3.ytimg.com/vi/Y8Wp3dafaMQ/hqdefault.jpg></a>">
</iframe>
```

Finally you'll notice that if we click the image it'll load the video but in a paused state and we would need to click it again to start watching. Fret not, cause the embed video URL supports player parameters and among those there's the autoplay variable which does exactly what you would expect. Additionally due to browser's default style users on systems with scrollbar—namely not macOS—will see an unnecessary scrollbar, but nothing that a small CSS reset wouldn't fix.

![Youbue Additional JavaScript](https://res.cloudinary.com/practicaldev/image/fetch/s--ESjkTlur--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://i.imgur.com/IT0tvqp.png)

```
<iframe width="560" height="315" src="https://www.youtube.com/embed/Id64silK_7M" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
```

