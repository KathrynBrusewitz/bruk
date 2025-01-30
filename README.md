# kathrynbrusewitz.github.io

Simple personal site. Static build generated with NextJS with TailwindCSS. See below for instructions for GH Pages:

## Export static site out of NextJS and host on GitHub Pages

I made the following changes in my NextJS project:

1. In `next.config.js`, the output type should be "export" and images should be set unoptimized if using Next/Image:
```
/** @type {import('next').NextConfig} */
const nextConfig = {
    output: "export",
    images: {unoptimized: true},
}

module.exports = nextConfig
```

2. Run `npm run build` (i.e. `next build`) to output HTML/CSS/JS to the directory `out`. 

3. After placing all the contents of `out` into this repo for hosting, I saw that only the content rendered. All the CSS, JS, and images were not being referenced correctly. To fix this, just add an empty file named `.nojekyll` as a sibling to the `_next` directory.
    - Why does this work? In this [article](https://www.viget.com/articles/host-build-and-deploy-next-js-projects-on-github-pages/), I learned that GitHub Pages ignores underscore-prefixed directories because Jekyll does, which is why it's skipping all the CSS and JS inside `_next`. Adding this file bypasses this default behavior.
    - To handle this automatically, I updated my build script: `"build": "next build && touch out/.nojekyll"`
