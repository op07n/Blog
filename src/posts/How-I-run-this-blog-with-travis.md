---
view: post
layout: post                          # Only in unique we use the "layout: post"
lang: en                              # Lang is required
author: op07n
title: How-I run this blog with travis
description: 
excerpt: 
cover: false                          # Leave false if the post does not have cover image, if there is set to true
coverAlt: 
demo: 
categories:
  - vuejs
tags: 
  - vuejs
  - vuepress
  - static site
created_at: 2019-06-19 09:00
updated_at: 2019-06-19 09:00
meta:                                 # If you have cover image

---

I forked this blog from [ktquez/vuepress-theme-ktquez-starter](https://github.com/ktquez/vuepress-theme-ktquez-starter) . I tweaked it a little bit to build it with https://travis-ci.org for free.

Here is what I did:

I use two repositories: https://github.com/op07n/Blog  and https://github.com/op07n/op07n.github.io.

The Blog repository is used to upload the new posts, and the other is automatically generated for travis-ci.

 I created a new repository called op07n.github.io and added a few files in  Blog repository:

*.travis.yml*

```yaml
language: node_js
node_js:
    - 8.12.0
cache: 
    directories:
        - node_modules
script:
    - chmod u+x deploy.sh
    - yarn deploy-ci
branch: master
```



*deploy.sh*

```bash
#!/usr/bin/env sh
set -e

yarn build

cd src/.vuepress/dist

git init
git add -A # 等价于 git add --all
git commit -m 'deploy'

git push -f https://${GH_TOKEN}@github.com/op07n/op07n.github.io.git master

cd -
```

I maid a few changes in *package.json:*

```json
{
  "name": "your-name-app",
  "version": "0.1.0",
  "description": "Descripton your webapp",
  "scripts": {
        "dev": "vuepress dev src",
        "build": "vuepress build src",
        "deploy": "~/bin/deploy.sh", 
        "deploy-ci": "./deploy.sh",
        "clean": "rm -rf dist"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/ktquez/vuepress-theme-ktquez-starter"
  },
  "keywords": [
    "vuepress",
    "vuepress-theme",
    "site",
    "blog",
    "theme-ktquez",
    "markdown",
    "static",
    "vuejs"
  ],
  "author": "Alan Ktquez <ktquez@gmail.com> (https://ktquez.com/)",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/ktquez/vuepress-theme-ktquez-starter/issues"
  },
  "homepage": "https://github.com/ktquez/vuepress-theme-ktquez#readme",
  "devDependencies": {
    "vuepress": "^0.14.2"
  },
  "dependencies": {
    "vuepress-theme-ktquez": "^0.2.18"
  }
}
```

 I copied *yarn.lock* from other site but I don't know if I really needed.

In my travis-ci account I wrote the GH_TOKEN variable with the token generated in my github account.

And with all these every time I write a new post the site in generated thanks to travis-ci



