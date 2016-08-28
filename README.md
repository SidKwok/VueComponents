# vue-components

> components with vue

## Noted

They are some components I may use during my job or, you know, fun stuff. And more important is that I can code for something to kill my time.

All components are supposed to be separated, which means there is no global dependencies such like `bootstrap.css'`. But it may includes some third-party like `moment`. I will inform in the docs if I use any third-party dependencies, please feel free to use them in your projects.

Each components may have a `readme` file in it, which is to explain how it works. It is actually more like a rule to force me to write docs after coding.

Punch me in the face if you can't find any docs in any components.

## Limits

 * Only works on `.vue` file, so I can't guarantee any other ways.
 * Should support IE9+.
 * Don't use css dependencies unless it is deadly necessary. Absolutely no global `css` like `bootstrap`.
 * Every component's style is `scoped`.
 * No preprocessor such like `sass` or `less`, only `css`.

## Dev step

```bash
npm install
npm run dev
```

If it can't work, try `sudo`. Then check it in `localhost: 3000`.

Done talking, time to code.

By the way, Vue is gas!
