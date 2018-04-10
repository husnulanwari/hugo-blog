---
title: "How To Create a Blog with Hugo and Github"
date: 2018-04-09T08:51:07+07:00
draft: false
---

## Introduction

Do you want to start a blog to share your latest adventures with various software frameworks? Do you love a project that is poorly documented and want to fix that? Or do you just want to create a personal website? But you don't have time to build it, setup the database, and creating a theme. The answer is [Hugo](https://gohugo.io) — with Hugo you could build your own blog in minutes.

[Hugo](https://gohugo.io) is one of the most popular open-source static site generators written in Go a.k.a [Golang](https://golang.org). It offers simplicity in building a website while maintaining a good performance and flexibility. Unlike other blogging platform, there is no database, no plugins requiring any permissions, and no underlying platform running on your server, there's no added security concern.

Themes — both the official ones that the Hugo team maintains as well as the community-contributed ones — has a wide range of selection that you can pick based on your need.

Some of the most popular choices include:

* [Ananke](https://github.com/budparr/gohugo-theme-ananke) - The intent of this theme is to provide a solid starting place for Hugo sites with basic features and include best practices for performance, accessibility, and rapid development.
* [Kube](https://github.com/jeblister/kube) - A professional and a responsive Hugo theme for developers and designers that offers a documentation section mixed with a landing page and a blog.
* [Creative portfolio](https://github.com/kishaningithub/hugo-creative-portfolio-theme) - A clean and elegant template mainly made for designers and creatives but can be easily transformed into a generic website.

You can find a more complete list of both official and community-contributed themes on Hugo's [website](https://themes.gohugo.io) and [Github](https://github.com/topics/hugo-theme).

In this tutorial, you'll install, and configure Hugo to generate static site as a blog. Next, you'll learn how to host your blog using Github Pages so everyone can access and read your awesome stories.

## Prerequisites

Before following this tutorial make sure you have:

* Git - You should have Git installed on your local machine. You can check if Git is installed on your computer and go through the installation process for your operating system by running `git --version` command. You'll see git version running on your machine otherwise you have to install git by following this [docs](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

* Github account - This is mandatory in order to host your site later on. Make yourself a Github account signing up on the front page.

* Text Editor - You need a text editor such as [VSCode](https://code.visualstudio.com), [Atom](https://atom.io), or [Sublime](https://www.sublimetext.com) to edit Hugo's configuration file and add some content to your site. If you are using Mac or Linux and looking for some heat you can use `nano` or `vim` text editor that comes out of the box

## Step 1 — Install Hugo

Note : In this tutorial I am using a Mac, if you are using Debian/Ubuntu or linux based OS you can follow Hugo's official [documentation](https://gohugo.io/getting-started/installing#linux).

Using [Homebrew](https://brew.sh), you can install Hugo with the following one-liner :

```shell
$ brew install hugo
```

Then verify your new installation by running this command :

```shell
$ hugo version
```

## Step 2 — Create a New Blog

Create a new site that will become your blog. Command below will create a new Hugo site in a folder named `delicious-blog`.

```shell
$ hugo new site delicious-blog
```

## Step 3 — Theme Your Blog

Next thing is to add some themes to your blog. With Hugo, you can either theme your blog yourself or use one of the beautiful, ready-made themes. I choose `cocoa` beacuse it is deliciolsly simple. To install it :

Make sure you are inside your blog directory :

```shell
$ cd delicious-blog
```

Clone `cocoa` theme into the `themes/cocoa` directory and copy `config.toml` file from `cocoa` to your site.

```shell
$ git clone https://github.com/nishanths/cocoa-hugo-theme.git themes/cocoa
$ cp themes/cocoa/exampleSite/config.toml ./
```

Adjust your site configuration by opening `config.toml` file using your favorite text editor. Fortunately `cocoa` gives a clear explanation line-by-line about this configuration.

If you want to add more themes, just repeat the above steps. For most themes it will works flawlessly.

## Step 4 — Add Some Awesome Content

There are more than one way you can create content for Hugo. The easiest way is to use Hugo's cli :

```shell
$ hugo new blog/my-first-post.md
```

This basicaly will create a `my-first-post.md` file inside `blog` folder (Hugo will create it automatically if doesn't exist) inside `content` folder. Edit the newly created content file if you want.

```
---
title: "How To Create a Blog with Hugo and Github"
date: 2018-04-09T08:51:07+07:00
draft: true
---

## Introduction

Do you want to start a blog to share your latest adventures with various software frameworks? YOUR CONTENT GOES HERE ...
```

In case you're curious, the generated file has a certain header to begin with — it called Front Matter. You can read more details about this [Front Matter](https://gohugo.io/content-management/front-matter) in Hugo's official documentation.

## Step 5 — Run Your Site Locally

Now, start the Hugo server with drafts enabled to see what's your site looks like :

```shell
$ hugo server -D
```

Navaigate your browser to [`http://127.0.0.1:1313`](http://127.0.0.1:1313) and see the magic 🎉. Apply different themes, tweak the configuration file and add more content until you satisfied with your result.

## Step 6 — Deploy to Github

It's not complete if your site just running on your machine, people still cannot access it yet. From their documentation, you can host your new Hugo website virtually anywhere. One of them is [Github Pages](https://pages.github.com), It's free, easy to setup and supports HTTPS!

1. Create a `<YOUR_PROJECT>` e.g (`delicious-blog`) repository with your Github account. This repository will hold all Hugo's content, configuration, and other files.

2. Create a `<USERNAME>.github.io` repository (Yes! You need two repository). Make sure your `<USERNAME>` is your real username, otherwise you site will not showing up properly. This repository will hold fully rendered version of your site.

    > Make sure your baseurl key-value in your site configuration reflects the full URL of your GitHub pages repository. e.g. `baseurl = https://<USERNAME>.github.io`

3. Inside your site directory, create a new git project and add a new remote url.
```shell
$ git init
$ git remote add https://github.com/<USERNAME>/<YOUR_PROJECT>`.git public
```

4. Remove public folder and add git [submodule](https://blog.github.com/2016-02-01-working-with-submodules/). So when you run hugo command to build your site it will lives on public folder but have different remote origin.
```shell
$ rm -rfd public/
$ git submodule add https://github.com/<USERNAME>/<USERNAME>.github.io`.git
```

5. Build your site and push everything to Github.
```shell
$ hugo -t cocoa
$ git add .
$ git commit -t 'Initital commit' && git push origin master
```
    Change directory to public, make commit and push everything in it. Note, this will publish into `https://github.com/<USERNAME>/<USERNAME>.github.io` repository.
```shell
$ cd public
$ git add .
$ git commit -t 'Initital commit' && git push origin master
$ cd ..
```

That’s it!

Your personal page should be up and running at `https://<USERNAME>.github.io` within a couple minutes.

## Conclusion

In this tutorial we downloaded, configured, and host a complete Hugo site. If you follow all the steps above you should see something like http://husnulanwari.github.io (this site). You can take a look it's source code at my [Github](https://github.com/husnulanwari).

If you'd like to learn more about how configure, customize your hugo site even further and see what else Hugo can do, visit the official Hugo [documentation](https://gohugo.io/documentation). You'll find a lot of resource starting from adding static page, comment, create your own theme and many more.

And, if you have an issue or idea to make Hugo better, feel free to contribute in their Github [repository](https://github.com/gohugoio/hugo).
