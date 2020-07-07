---
title: "Personal website with Jekyll and Minimal Mistakes theme"
categories:
  - Blog
tags:
  - Jekyll
  - Minimal Mistakes remote theme starter
---

I was thinking about hosting my website for some time and after looking around, I finally settled with [Jekyll](https://jekyllrb.com/) for my static site. Here I would like to point that I am somewhat familiar with web development but both Ruby and Jekyll are new to me. I will use this document to record the steps for hosting my site.

## Step Zero - What do I want?
I want is a static website that is easy to create, host, and update. It would host info about me, and occasionally my thoughts, creations, and comments. I am not much into web-development so I would like to use a decent template that I can build upon. I would also like the possibility of having comments on my website. 

## Step One - Choosing a starting point
After some research, I decided to use [Jekyll](https://jekyllrb.com/) for my static site. Once I settled with Jekyll, I read through their [step by step tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) to understand the basic of Jekyll. I also looked for other resources and choose a template. So this post tells the story of how I step up [Minimal Mistakes Jekyll theme](https://github.com/mmistakes/minimal-mistakes).

## Step Two - Minimal Mistakes remote theme starter
Instead of hosting the website on my own server, I decided to use Github pages to host it. So I used the [**Minimal Mistakes remote theme starter template**](https://github.com/mmistakes/mm-github-pages-starter/generate), as they recommend it for easy hosting with Github pages. Starting with the template was easy, just had to click on the link. Next, I updated some of the values in the _config.yml as [documented](https://mmistakes.github.io/minimal-mistakes/docs/configuration/) here. Okay, this is where I had my first issue with this template. I expected to be able to see the effect of changes I made in real-time, just to see how would the changes look on the website. And it took me some time to find how to do it. Here is what I finally did:
1. Install the dependencies locally using `bundle install --path vendor/bundle`
2. Build and serve locally using `bundle exec jekyll serve`
3. Preview local build at http://127.0.0.1:4000


So far so good! I was able to run everything locally and see the effect of my changes. 

## Step Three - Add a custom category

After adding basic info about me, I wanted to add a category for my publications. This was proved to be a bigger hurdle than I thought. What I didn't realize the in beginning is that the **Minimal Mistakes remote theme starter template** hides all the layout files from the user. Which is great if you stick to the original template, but problematic as soon as you want to customize the layout. I think there are ways to customize the template, but at least at the moment they seem like too much of a hassle and I decided to re-consider my original choice of starting with the theme starter and instead decided to fork the template and starting from scratch.

___

# A fresh start!

## Step One - Choosing a starting point
So this time, I started by forking the [minimal-mistakes](https://github.com/mmistakes/minimal-mistakes) repo. 

## Step Two - Minimal Mistakes base version
Firstly, I removed the following files as per the [documentation](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/).   
`rm -rf .editorconfig .gitattributes .github ./docs test CHANGELOG.md minimal-mistakes-jekyll.gemspec README.md screenshot.png screenshot-layouts.png`

Next, I fixed the Gemfile and added install-dependencies as per [instructions here](https://mmistakes.github.io/minimal-mistakes/docs/installation/#install-dependencies). Following the pro-tip, I used a bleeding edge version of this gem, via `gem "minimal-mistakes-jekyll", :github => "mmistakes/minimal-mistakes".` Then as before, I used the following commands.

1. Install the dependencies locally using `bundle install --path vendor/bundle`
2. Build and serve locally using `bundle exec jekyll serve`
3. Preview local build at `http://127.0.0.1:4000`

The base version looks great! It has some extra files but now I understand the function of most of them.

## Step Two - Minimal Mistakes customization
So now I would like to customize the base version with info. So I copied the `_config.yml` from the last iteration and tried to build it again. However, it did not work and it threw the following error message. 
`Dependency Error: Yikes! It looks like you don't have jemoji or one of its dependencies installed.`

Instead, I started with `_config.yml` that was originally in the repo and edited it for personal use. This solved this issue and I could proceed forward. 

Next, I edited the `./_data/navigation.yml` and I added four paths namely, publications, posts, about me, and sitemap. I build the site again and four options appeared in the navbar. However, this is where I also ran into another issue. If you click on the link, the page did not exist. I thought that it would load it from the `_layouts/` but I was wrong. So after looking around the code for [docs on minimal mistakes](https://github.com/mmistakes/minimal-mistakes/tree/master/docs), I realized I am missing the `_pages` which should link `_data/navigation.html` to `_layouts/`. I found it very confusing that it could generate the home page without the `_pages` directory. Why is the home page special? Moreover, I can not find an explicit link between `_pages` and `_layouts/`. In the `_config.yml`, I found `include: - _pages`, but how does that link the `./_data/navigation.yml` with the `_layouts/`. Is it the permalink in the `_pages/` that does the trick?  If you know the answer, leave a comment below!

The good thing here is that the `_pages` can be written in markdown, while the `_layouts/` can be in Html. So the pages are rather easy to setup. So I set up my first page based upon the examples [here](https://github.com/mmistakes/minimal-mistakes/tree/master/docs/_pages).

My goal for me was to host my list of publications. Now, the design decision was to whether have a `_posts/` like setup for publications, where every publication is somewhat like an independent post with the possibility of comments from others or simply have a static list of publications without a possibility of comments on each publication. In the end, I decided to go for a simple list written in markdown. I may revisit this decision later. 

I added publications to `_pages/publications.md`. Here is the header of that file.

    ---
    title: "Publications by Year"
    permalink: /publications/
    layout: archive
    author_profile: false
    ---
    Below, you will find my list of publications 
    * Publication 1
    * Publication 2

This basically completes the basic setup and I have the minimum version that can be pushed to Github pages. 

## Step Three - Comments with staticman

I really like the idea of [Staticman](https://staticman.net/) but it seems that I will need to host it myself. So I will add comments on some other day. Here are two resources that I found useful on [using staticman with this theme](https://mademistakes.com/articles/improving-jekyll-static-comments/) and [self hosting staticman API](https://www.datascienceblog.net/post/other/staticman_comments/).


## Step Four - Hosting on Github pages

To host on Github pages, I pushed the changes and renamed the repo to ankitkariryaa.github.io. It worked wonderfully in the first attempt!


## Summary 
So far I have really enjoyed working with Jekyll and Minimal Mistakes theme. In the next iteration, I would like to improve the home page so both publications and posts appear there (maybe I will limit to selected items). Also, I would like to enable comments using Staticman. Another thing is that search currently does not work in the publications. Till next time!



