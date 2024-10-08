https://davidwalsh.name/fixing-cumulative-layout-shift-problems-on-davidwalshblog


# CLS
It is a metric for how fast a website is.

It doesn't measure how fast it loads, instead it measures how much the page shifts during loading.

## How to measure Core Web Vitals
Don't use google lighthouse - it only does a single test from a fast connection. Users might have a different experience.

## Biggest culprit of bad CLS
The most common problem is that images are set to 0x0 pixels when downloading (the browser doesn't know how big the image is going to be)

Then later when the image is downloaded the element is resized. The way to fix this is by setting the width and height of the image directly on the element.

```html
<img src="..." width="800" height="800" />
```