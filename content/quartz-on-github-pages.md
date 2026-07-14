---
title: Quartz as a SSG for Obsidian
language: english
date: 2024-09-23
draft: false
tags:
  - quartz
  - github-pages
  - "#obsidian"
---
Once I [took the decision to start my blog](index), I had to overcome any friction to publish content without complex setups. I had decided which authoring platform to work with, [Obsidian](https://obsidian.md/). It was the time to choose a good static-site generator. After reading pro's and con's, I decided on [Quartz](https://quartz.jzhao.xyz/).

This is how I made my blog's initial set up.

## Quartz
 
On the console, cloned the project by typing 
```bash
git clone https://github.com/jackyzha0/quartz.git
```

Before cd'ing the project directory, during a very lucid and inspired moment, I renamed it to the specially creative name `my-blog`
```bash
mv quartz my-blog
cd my-blog
```

I followed the installation instructions, setting previously the desired node version (Quartz needs v20 at least)
```bash
nvm use 20
npm i
npx quartz create
```

The last command asks the user two questions for configuring the project. In my case, I chose the following options:
- **Choose how to initialize the content in `./my-blog/content`**: *Empty Quartz*
- **Choose how Quartz should resolve links in your content**: *Treat links as shortest path*

## Obsidian

In this case, I simply started a new vault called `my-blog` and set the vault directory to `my-blog/content`. Time will tell if setting the `content` directory was a good or bad decision. My purpose was to avoid any distraction and show only the files I am interested in, for publishing, and nothing else.

## Github

#### Creating new repository
I created a **new repository** on Github and named it `my-blog`, **leaving the rest of all controls of options to their default state**.

#### Setting up Github Pages
I accessed the Github Pages settings page, by following the menus
>`Settings` > `Pages`

and switched the **Build and deployment - Source** selector to `GitHub Actions`.

Finally I downloaded and applied ["the right" CICD patch file](https://gist.github.com/mtribal/795abd0acb4b0dbf4bdd226c4cd38157) for building the content to their static-site appearance and deploying it to Github Pages platform
```bash
curl https://gist.githubusercontent.com/mtribal/795abd0acb4b0dbf4bdd226c4cd38157/raw/16e58cf07f0097217d43887067041025632f2849/deploy.yaml -o .github/workflows/deploy.yaml
git add .github/workflows/deploy.yaml
```

## Deploying

It was almost set! I needed only set the correct remote reference in the current repository and make my first deploy

```bash
git remote set-url origin git@github.com:mtribal/my-blog.git
npx quartz sync --no-pull
```

After impatiently checking for no more than one minute the pipeline execution in Github Actions, the seed of my future blog was finally planted. Hooray!
