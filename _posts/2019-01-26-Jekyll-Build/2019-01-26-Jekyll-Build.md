---
title: Build Your Blog with GitHub Pages
tags: Jekyll blog
edit: 2019-01-26
categories: Jekyll
status: Paused
mathjax: true
highlight: true
mermaid: true
description: Build Your Blog with GitHub Pages. You can use my theme `PointingToTheMoon` to write your blog or other themes. My theme is great for academic use, for it features simple post page with mathjax support and a side bar with toc. The main page on the other hand is somewhat fancy.
---



# Why GitHub Pages?

1. It's simple.

   1. The Domain is just `username.github.io`. You don't need to buy your own domain. PS, All domains must be registered by the owner with ID. So that saves you a ton of trouble. But GitHub pages also allows you to 
   2. GitHub pages build the website for you. This means you don't need to install `jekyll` or `ruby`, you don't need you locally build your website and publish it. You just commit your source code and that's all. 
   3. After properly configured, you can write in `markdown`, and `push` (a fancy name for upload) to GitHub.  Things like equations, lists, tables, mermaid-diagrams, images, or videos are automated supported. This means all you'll need is a text editor as simple as good old notepad.exe to write your post, yet I strongly recommend [`typora`](https://www.typora.io/). As the time of writing, it is free.

2. You have absolute control over anything.

   1. The look. WordPress, blogspace as well as other services does provide good-looking templates. But some of them have unnecessary constrains of where to put what. While on GitHub, you get to control what your pages look like. Still, there are thousands of readily made themes at your disposal if you are lazy. With a few modifications, you can tailor your website the way you want.
   2. Functions. RSS feed, search, table of contents, pagination, visitor analysis, commenting, *etc*. anything you can think of it out there. GitHub is a static site generator, which means there are no server side calculations. But you can always trick the users with a few walk-arounds and CDNs.

3. There is a nice touch. GitHub's famous for being used by techies.

   Having your own website built entirely by yourself.

4. Limitations

   GitHub Pages source repositories have a recommended limit of 1GB. Published GitHub Pages sites may be no larger than 1 GB. GitHub Pages sites have a soft bandwidth limit of 100GB per month.	GitHub Pages sites have a soft limit of 10 builds per hour. See [here](https://help.github.com/articles/what-is-github-pages/#usage-limits)

# About Jekyll

What is Jekyll

Jekyll is a simple free blog generation tool that converts plain text into static websites and blogs; since our GitHub Pages generate static pages, each time you update your blog, you need to manually change the HTML, which makes every time you write a blog. It becomes very cumbersome, and after using this tool, it will generate blog content according to the preset format, you don't need to care about the html code, just focus on the blog writing.

# About Git

What is Git

Git is an open source distributed version control system that can efficiently and quickly handle project version management from very small to very large. Its function is similar to Svn, it is a version control tool, which can be used to write the code we write and submit our code to Github.

I am going to assume that you know the basic operations of git.[Git common command summary](https://blog.csdn.net/tomatozaitian/article/details/73515849) If not, just download the [GitHub Desktop](https://desktop.github.com/), and do everything in GUI. For the most of bloggers, only commit and push is required. For you to publish your work, save your file in your editor, go to GitHub Desktop, commit your changes, and push.

The main interface is like this:
<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-26-Jekyll-Build/assets/Main%20interface.png" width="70%">

You can use `GitHub Desktop` to clone your repositories,save the GitHub homepage repository to your local.
<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-26-Jekyll-Build/assets/clone1.png" width="70%">
<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-26-Jekyll-Build/assets/clone2.png" width="70%">

After you edit your project in local then commit your changes
<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-26-Jekyll-Build/assets/commit.png" width="70%">

Finally uploaded to GitHub,push!
<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-26-Jekyll-Build/assets/push.png" width="70%">

# General Process
1. Log in to your Github account
2. Create a new repository to save personal website project
3. Upload a completed personal website to Github
4. After the upload is successful, visit your homepage based on the domain name.

Specific operations can refer to the following link:

[手把手教你在Github上建立自己的个人博客网站](https://blog.csdn.net/u012168038/article/details/77715439)

[使用Hexo+Github一步步搭建属于自己的博客](https://www.cnblogs.com/fengxiongZz/p/7707219.html)

[Github搭建个人博客](https://blog.csdn.net/xudailong_blog/article/details/78762262)

# What Should I Modify ( If you choose my theme project )

Here is a list of files you need to modify

1. License.md: add your version of license at the beginning of the file.
2. Readme.md: add your description.
3. config.yml: fill in as much as you can.
4. index.html: fill in description and (if any) proposed posts.
5. register at [commentit.io](https://commentit.io/). This enables your website's comment feature.
6. Better google discovery: google site authentication. Just go to [webmaster](https://search.google.com/search-console?hl=en) and click `add property` and download the google authentication file, put in under the root of your repo. A few days later, you should be able to see your website in google search by searching `site:your-site-name.github.io` (no space in between).

After that, you should be able to enjoy your blogging!