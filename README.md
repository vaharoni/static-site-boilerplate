# Static website boilerplate

This repo is a template of a static website that supports internationalization using Jekyll, esbuild, and Tailwind CSS.
Ready to use with Github Pages.

## Contents

- [Jekyll](https://jekyllrb.com/) and 
[Jekyll Multiple Languages](https://github.com/kurtsson/jekyll-multiple-languages-plugin) for static HTML generation
- [esbuild](https://esbuild.github.io/) for Javascript bundling
- [Tailwind CSS](https://tailwindcss.com/) for auto-generating CSS utility classes
- A base layout and a sitemap that supports i18n by generating alternate language links  
- A [Github action](https://docs.github.com/en/actions) that runs the build pipeline in production, 
enabling Jekyll plugins that Github does not support by default
- Utility scripts to run the build pipeline in development 

## Serving your site in production

When forking, remember to:
- update the `baseurl` entry in [docs/_config.yml](docs/_config.yml) so that your links point to the right location
- if you're using Github Pages to serve the website from a custom domain, add a `docs/CNAME` file with your 
domain (e.g. `www.example.com`). Refer to [Github's documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
on custom domains.

To serve ths site using Github pages, go to the Repo's Settings > Pages, and update the Source option to the 
root directory of the `gh-pages` branch. This branch is updated automatically by the build pipeline every time you
push an update to the `main` branch. 

## CSS

To add common styles to DOM elements, update 
[docs/assets/stylesheets/tailwind.css](docs/assets/stylesheets/tailwind.css) per 
[Tailwind's documentation](https://tailwindcss.com/docs/adding-custom-styles#using-css-and-layer).

To DRY components that rely on many Tailwind CSS classes, you could:
- render them in HTML by creating the `docs/_includes` folder and following [Jekyll's documentation](https://jekyllrb.com/docs/includes/) on includes
- render them in Javascript using a library like React

## Javascript

Thanks to esbuild, you can use ES6 and CommonJS modules, Typescript, and React out of the box.
Add javascript files to the `docs/assets/javascripts` folder, and import them into `app.js` as usual.
They will all be bundled into a single `docs/_site/assets/javascripts/main.js` file that the base layout includes.

To add a javascript library, run `yarn add ...` and import it in your javascript files.

## Jekyll plugin

To add a Jekyll plugin, run `bundle add ...` per the plugin's instructions and load it by updating the `plugins`
entry in `docs/_config.yml`.

## Sitemap

The [sitemap.xml](docs/sitemap.xml) file generates I18n alternate links. It is quite basic.
If you need more control over the last modified or change frequency fields,
refer to [this article](http://www.independent-software.com/generating-a-sitemap-xml-with-jekyll-without-a-plugin.html)
or use one of the sitemap plugins for Jekyll.

## The build pipeline

When pushing changes to the `main` branch on Github, the [.github/workflows/build.yml](.github/workflows/build.yml) 
Github Action runs the [bin/build](bin/build) script, and commits the resulting files in `docs/_site` into 
the `gh-pages` branch at its root. Check out the `gh-pages` branch on this repo to see what the output looks like.

[bin/build](bin/build) performs the following:
- Jekyll processes files in the `docs` folder, generating static files in `docs/_site`
- esbuild bundles [docs/assets/javascripts/app.js](docs/assets/javascripts/app.js) to `docs/_site/assets/javascripts/main.js`
- Tailwind bundles [docs/assets/stylesheets/tailwind.css](docs/assets/stylesheets/tailwind.css) to `docs/_site/assets/stylesheets/main.css`

## Local development

Run [bin/dev](bin/dev) to have Jekyll, esbuild, and Tailwind watch for files and recreate `docs/_site` using Foreman.
Your site is served from [http://localhost:4000](http://localhost:4000) using Webrick as usual.
