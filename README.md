# Static website boilerplate

Boilerplate for a static website that supports internationalization using Jekyll, esbuild, and Tailwind CSS.
Ready to use with Github Pages.

When forking, remember to:
- update the `baseurl` entry in `docs/_config.yml`
- update the `author` entry in `package.json`
- if you're using Github Pages to serve the website from a custom domain, add a `docs/CNAME` file with your domain (e.g. `www.example.com`)  

## Contents

- [Jekyll](https://jekyllrb.com/) and 
[Jekyll Multiple Languages](https://github.com/kurtsson/jekyll-multiple-languages-plugin) for static HTML generation
- [esbuild](https://esbuild.github.io/) for Javascript bundling
- [Tailwind CSS](https://tailwindcss.com/) for auto-generating CSS utility classes
- A base layout and a sitemap that supports i18n by generating alternate language links  
- A [Github action](https://docs.github.com/en/actions) that runs the build pipeline in production, 
enabling Jekyll plugins that Github does not support by default
- Utility scripts to run the build pipeline in development 

## The build pipeline

When pushing changes to the `main` branch on Github, the `.github/workflows/build.yml` Github Action runs `bin/build`,
and commits the resulting files in `docs/_site` into the `gh-pages` branch at its root.

`bin/build` performs the following:
- Jekyll processes files in the `docs` folder, generating static files in `docs/_site`
- esbuild bundles `docs/assets/javascripts/app.js` to `docs/_site/assets/javascripts/main.js`
- Tailwind bundles `docs/assets/stylesheets/tailwind.css` to `docs/_site/assets/stylesheets/main.css`

## Local development

Run `bin/dev` to have Jekyll, esbuild, and Tailwind watch for files and recreate `docs/_site`.
Your site is served from [http://localhost:4000](http://localhost:4000) using Webrick as usual.
