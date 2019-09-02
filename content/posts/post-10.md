---
template: SinglePost
title: Lazy Loading Youtube Videos
status: Published
date: '2018-03-28'
featuredImage: >-
  https://ucarecdn.com/69bcae44-f555-4b56-b08e-bd0f2013654a/-/crop/1634x1690/0,434/-/preview/
excerpt: Lazy Loading YouTube Videos
categories:
  - category: JavaScript
meta:
  description: test meta description
  title: Web Best Pratices | Lazy Loading Youtube Videos
---

The thing is the job was specifically to deliver high performance, accessibility and modern practices, so you can imagine my annoyance when I noticed that just for having this <iframe> I got this:
  
  Plus a few extra requests that my ad blocker handled for me.

That is over 500KB that my users would have to download on top of the website, regardless if they'll watch the video. Do you have any idea how heavy this might hit your users, specially the ones with slow connection or low performing machines? To add insult to injury they'd also be being tracked—Hi Google—for just loading a video they didn't even know was there.

It being a simple static website I wanted to keep my solution to a minimum, so here's what I came up with.

The code for embedding an YouTube video, as of August 2019, goes like this:

```javascript
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

```html
<a href="https://www.youtube.com/embed/Y8Wp3dafaMQ">
  <img src="https://i3.ytimg.com/vi/Y8Wp3dafaMQ/hqdefault.jpg">
</a>
```

Cool, but I really don't want to have to create a whole new page just for this teeny tiny snippet of code. Well, we're in luck cause <iframe> has just the perfect thing for us—the srcdoc attribute. With it you can source the <iframe> directly in the hosting page. Just beware that it won't work on Edge or IE and that we can't use double quotes.

```html
<iframe 
  ...
  srcdoc="<a href=https://www.youtube.com/embed/Y8Wp3dafaMQ><img src=https://i3.ytimg.com/vi/Y8Wp3dafaMQ/hqdefault.jpg></a>">
</iframe>
```

Finally you'll notice that if we click the image it'll load the video but in a paused state and we would need to click it again to start watching. Fret not, cause the embed video URL supports player parameters and among those there's the autoplay variable which does exactly what you would expect. Additionally due to browser's default style users on systems with scrollbar—namely not macOS—will see an unnecessary scrollbar, but nothing that a small CSS reset wouldn't fix.
