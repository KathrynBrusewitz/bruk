# kathrynbrusewitz.github.io

Personal website.

Build output generated with NextJS with TailwindCSS. This also sets up the project for future features, such as an admin login, CMS for writing, and data visualizations that I want to experiment with.

This only needs to be a static one page site for the short term.

## Export static site out of NextJS and host on GitHub Pages

I needed to make the following changes in my NextJS project in order for GH Pages to host this really simple site correctly:

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

3. After placing all the contents of `out` into this repo for GitHub to host it, only the content rendered. All the CSS, JS, and images were not being referenced correctly. To fix this, just add an empty file named `.nojekyll` as a sibling to the `_next` directory.
    - Why does this work? In this [article](https://www.viget.com/articles/host-build-and-deploy-next-js-projects-on-github-pages/), I learned that GitHub Pages ignores underscore-prefixed directories because Jekyll does, which is why it's skipping all the CSS and JS inside `_next`. Adding this file bypasses this default behavior.
    - To handle this automatically, I just updated my build script to: `"build": "next build && touch out/.nojekyll"`
