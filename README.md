# vue-components

> components with vue

## Noted

 * They are some components I may use during my job or, you know, fun stuff. And more important is that I can code for something to kill my time.

 * All components are supposed to be separated, which means there is no global dependencies such like `bootstrap.css'`. But it may includes some third-party like `moment`. I will inform it in the docs if I use any third-party dependencies, please feel free to use them in your projects.

 * Remember that if you apply some global css such like `button {color: red}`, the component may not perform in a correct way. In this time, feel free to change it in the component. It should be easy to understand its structure.

 * Each components may have a `readme` file, which is to explain how it works. It is actually more like a rule to force me to write docs after coding.

 * Only works on `.vue` file, so I can't guarantee any other ways.

 * Fully tested with `Vue@1.0.26`, can't guarantee a dime on `Vue@2.0.0`.

 * Should support IE9+.

 * Punch me in the face if you can't find any docs in any components.

## Guide

 * Each component is in `./src/components`.
 * Before you use the component you are supposed to `import` it in to your project:
 ```javascript
 // A super easy example
 import Aside from './components/Aside/Aside';
 ...
 components: {
     Aside
 }
 ```
 * Each component is separated in a individual file folder.
 * Please have a peak of `readme` before you use them.
 * Dev step:
 ```bash
 npm install
 npm run dev
 # Check it in `localhost: 3000`.
 # If it can't work, try `sudo`.
 ```

## Limits (to me)

 * Don't use css dependencies unless it is deadly necessary. Absolutely no global `css` like `bootstrap`.
 * Every component's style is `scoped`.
 * No preprocessor such like `sass` or `less`, only `css`.
 * Have animations' doubt? Find out in `Animate.css`!

Done talking, time to code.

By the way, Vue is gas!

git test
