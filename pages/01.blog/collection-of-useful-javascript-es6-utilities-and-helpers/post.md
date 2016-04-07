---
title: 'Javascript ES6 Utilities: Tiny script to detect Media Queries'
---

Almost every web project I get involved with I end up reusing parts of code to kick-start things. It is widely accepted to use reset.css, normalize.css, and internet is full of styling pre-processor mixins, helpers, functions and other universal chunks of code.

Javascript is no different, but with a slight twist – there are so many node package modules out there that we some time use entire libraries to achieve something quite simple. I recently stumbled upon few small snippets that solved problems that I previously used libraries to deal with. 

I am starting the post series **Javascript ES6 Utilities** and I present you the first script: 


##Breakpoint detection via Javascript (through CSS)
You know those moments when you need to load specific scripts based on your screen size, for example on mobile load extra scripts to handle nesting of navigation, while on desktop this needs to be entirely different? No sweat, there are plenty of ways to do that, either use `matchmedia` or rely on a library like [enquire.js](http://wicky.nillia.ms/enquire.js/ "Enquire.js"). They probably need a polyfill or some other way to deal with legacy browsers. 

There is a better way - simple, yet effective, use css to output media query names on html tag as content and then grab them with js:
```css
html {
  &::after {
    content: "small";
    display: none;

    @media only screen and (min-device-width: 768px) 
      content: "medium";
    }

    @media screen and (min-device-width: 1200px) 
      content: "large";
    }
  }
}
```
The only thing you need to do now is to grab the breakpoint names with javascript:
```javascript
module.exports = {
 /* Get active breakpoint */
  getActiveBreakpoint: function() {
    return window.getComputedStyle(document.documentElement, ':after').getPropertyValue('content').replace(/['"]/g, '');
  }
}

getActiveBreakpoint() // Outputs small, medium or large
```
And voila! You got your breakpoints. Rest is up to you.