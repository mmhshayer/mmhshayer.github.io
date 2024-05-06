---
author: "Mohammad Mustakim Hassan"
title: "Deploying a JAMstack Blog with Hugo, PaperMod, GitHub Actions, and GitHub Pages"
date: "2023-08-28"
description: "Learn how to deploy a JAMstack blog using Hugo, PaperMod theme, GitHub Actions, and GitHub Pages."
tags: ["frontend","Hugo", "GitHub Actions", "GitHub Pages"]
ShowToc: true
---
## Introduction

In this comprehensive guide, we'll dive into the exciting world of JAMstack development by leveraging the power of Hugo, a lightning-fast static site generator. By combining Hugo with the stylish PaperMod theme, harnessing the efficiency of GitHub for version control, automating deployment using GitHub Actions, and hosting your creation on GitHub Pages, you'll be well on your way to crafting and sharing a dynamic and seamless blog. Let's embark on this journey to streamline your blogging process!

---

## Prerequisites

Before diving in, let's ensure you're well-prepared:

1. `Git installed`: If you don't have Git installed, you can [download and install](https://git-scm.com/downloads) it from the official website.
2. `GitHub Account`: [Create an account](https://github.com/) if you don't have one.
3. `Hugo`: Install Hugo by following the [official installation guide](https://gohugo.io/installation/).

---

## Building a Blog with Hugo

### Create a New Hugo Site

Start by creating a new Hugo site using the following commands:

```bash
hugo new site <name-of-site> -f yml
cd <name-of-site>
```

---

## Managing Git Branches

It is a good practice to create a new branch for each new feature you add to your project.

### A branch for development, version control

create a new branch called `dev` and switch to it:

```bash
git checkout -b dev
```

### A branch to deploy the site

create new branch called `gh-pages`:

```bash
git branch gh-pages
```

### A branch for writing and drafting posts

create a new branch called `posts`:

```bash
git branch posts
```

> Don't forget to publish the branch to the remote repository
---

## Managing Themes

Instead of developing a theme from scratch, the easiest way to get started is to use an existing theme. I will use [PaperMod](https://github.com/adityatelange/hugo-PaperMod) as the theme for this project.
> Inside the folder of your Hugo site, run:

### Adding a theme as a submodule

```bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

### Re-cloning the repo

when you clone the repo, you will see that the theme folder is empty. To get the theme files, you need to run the following command:

```bash
git submodule update --init --recursive
```

### Updating the theme

To get the latest version of the theme, use the following command:

```bash
git submodule update --remote --merge
```

### Configure the Theme

You can follow the official guide to configure the theme. [PaperMod](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation##sample-configyml)

> To configure the theme, you need to add the following lines to the `config.yml` file:

```bash
theme: PaperMod
```

### Run development server

While in development, you will be able to see all draft posts also:

```bash
hugo server -D
```

---

## Automating with GitHub Actions

This workflow sets up Hugo, builds your site, and deploys it to the gh-pages branch.

### Create a GitHub Actions Workflow

In your repository, create a `.github/workflows` directory if it doesn't exist. Inside the `workflows` directory, create a file named `deploy.yml`:

```bash
name: Deploy Site

on:
  pull_request:
    types: [closed]
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-22.04
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          submodules: true
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.91.2'

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: ${{ github.event.pull_request.merged == true && github.event.pull_request.base.ref == 'main' }}
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

### Generate GitHub Personal Access Token

Go to your GitHub Account Settings > Developer Settings > Personal access tokens.
Generate a new token with the "repo" scope.
Copy the generated token.

### Add the Token as a Secret

In your repository, go to Settings > Secrets.
Create a new secret named ACTIONS_DEPLOY_KEY and paste the token as the value.

---

## Sharing Your Thoughts with the World

### Create a New Post

To create a new post, run the following command:

```bash
hugo new posts/<name-of-post>.md
```

### Add Content to the Post

Start by adding the following lines to the post file:

```bash
---
author: "Me"
title: "A new post"
date: "2023-05-17"
description: "A brief description of the post"
tags: ["frontend", "web"]
ShowToc: true
---
```

Add content below the metadata section:

```bash
# Introduction
lorem ipsum
```

### Save the Post to github

commit and push to the 'post' branch of remote repository

```bash
git add .
git commit -m "add new post"
git push origin posts
```

---

## Publishing

### Create and merge pull request to "main" branch

- Create a pull request to merge the "posts" branch to the "main" branch
- Merge the pull request
- Delete the "posts" branch

### Await Deployment
>
> await the deployment ot finish. you can see the progress in "Actions" tab of your repo.

### View the Deployed Site
>
> You can see the deployed site at:

```bash
https://<your-github-username>.github.io/<repo-name>/
```

---
