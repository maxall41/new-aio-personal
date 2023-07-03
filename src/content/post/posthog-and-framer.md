---
title: Using Framer with Posthog
description: A super short article about using posthog with Framer
publishDate: "2 Jul 2023"
tags: ["Software"]
---


If you are using Framer to quickly throw together a landing page, you are probably going to want better analytics than what Framer offers by default. Personally, my favorite analytics tool for landing pages is Posthog. But when using the Posthog toolbar with Framer you run into an issue where Framer removes the Posthog query string from the URL before it can get passed into Posthog. This means that if you just paste in the default Posthog analytics snippet the toolbar will not work. This is a known issue that can be fixed by adding:
```js
const toolbarJSON = new URLSearchParams(window.location.hash.substring(1)).get('__posthog')
if (toolbarJSON) {
 posthog.loadToolbar(JSON.parse(toolbarJSON))
}
```
But wait. This doesn't work because Posthog has not been fully initialized by the time we call `loadToolbar`. My solution which is admittedly  janky is to just add a small delay and do something like this:
```js
const toolbarJSON = new URLSearchParams(window.location.hash.substring(1)).get('__posthog')
if (toolbarJSON) {
    setTimeout(() => {
        posthog.loadToolbar(JSON.parse(toolbarJSON))
    },500)
}
```
There is probably a better way todo this. But it worked for me and is good enough in 99.99% of use cases. So...
