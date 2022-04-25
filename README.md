# My Personal site

Github repo for my personal site.

Build with Hugo, using the papermod theme.

## modifications

Some modifications are made:

- index_profile: removed the title, added the subtitle section
- svg: added a home and book icon
- links: add a link template

## to-do

## technical

- [x] enable github pages
- [x] create azure DNS for callebaut.io
- [x] enforce https
- [x] github actions to deploy hugo
    - [x] split build and deploy
- [x] add tags and packages
    - [x] add app insights annotations
- [x] prettify commit messages on gh-pages deploy
- [ ] integrate [html test](https://github.com/wjdp/htmltest)
- [ ] integrate [pa11y](https://pa11y.org) accessibility test
- [x] add application insights for observability
    - [x] templatize app insight integration (config and partial templates)
 
## website

- [x] change theme to [paperMod](https://themes.gohugo.io/hugo-papermod/)
- [x] enable auto dark\light mode
- [x] add blog section
  - [x] add series links
  - [ ] enable blog
  - [ ] enable comments via GH issues (https://utteranc.es)
  - [ ] enable archive and search
- [x] add favicons
- [x] validate twitter cards
- [x] validate opengraph cards
- [x] add links to other resources \ blogs
  - [x] create data file
  - [x] create template
  - [x] link content page
- [x] Mozilla observatry
  - [x] content security policy
  - [x] HTTP strict transport security
  - [x] X-Content-Type-Options
  - [x] X-Frame-Options
  - [x] X-Xss-Protection
- [x] [pagespeed](https://pagespeed.web.dev/report?url=https%3A%2F%2Fcallebaut.io%2F)
  - [x] properly size images
  - [x] serve images in next-gen format
  - [x] specify explicit width and height
- [x] html encode emoji's

