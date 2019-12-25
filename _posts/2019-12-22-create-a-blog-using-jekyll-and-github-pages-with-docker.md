---
layout: post
title: Create a blog using Jekyll and GitHub pages with Docker
---

This is a complete guide for blog creating with Jekyll and Docker. Jekyll is a static site generator that you can use to create simple sites or blogs and Github pages is a static site hosting service. With Docker, it could compile or even serve a Jekyll site locally without going through the entire fuss of getting Jekyll up and running on a local machine.

# Prerequisites
- mac
- A GitHub account

# Goal
This is what the website we make will look like:

![example website]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-24 at 19.21.02.png)

# 1 Create a Jekyll blog
reference: [https://davemateer.com/2018/01/25/Jekyll-and-Docker](https://davemateer.com/2018/01/25/Jekyll-and-Docker)
## 1 Learn Jekyll and Theme
[Jekyll](https://jekyllrb.com) is a website generator that’s designed for building minimal, static blogs to be hosted on GitHub Pages.

There are multiple ways to get started with Jekyll, each with its own variations. Here are a few options:
* Install Jekyll locally via the command line, create a new plane website using `jekyll new`, build it locally with `jekyll build`, and then serve it.

* Clone a repository as a starting point to your local machine, install Jekyll locally via the command line, make updates to your website, build it locally, and then serve it. (in this guide, Jekyll will be installed on docker)

In this guide, the theme, [Jekyll Now](http://www.github.com/barryclark/jekyll-now) will be used as a starting point.

## 2 Learn Git, GitHub and GitHub Pages
[Git](https://git-scm.com) is the most widely used modern version control system in the world today.

[GitHub](https://github.com) is a Git repository hosting service, but it adds many of its own features. While Git is a command line tool, GitHub provides a Web-based graphical interface.

[GitHub Pages](https://pages.github.com) is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub, optionally runs the files through a build process, and publishes a website.

## 3 Set up Git
Follow instructions on [Set up Git](https://help.github.com/en/github/getting-started-with-github/set-up-git#setting-up-git) on GitHub manual.  

## 4 Set up GitHub account
Set up GitHub account with the [official guide](https://help.github.com/en/github/getting-started-with-github/signing-up-for-a-new-github-account).

## 5 Clone a starting point
We’ll start by cloning the repository, Jekyll Now, that has followed best practices. This will get us on the right track and save a lot of time.

Open terminal on mac.

Run below command in wherever you want.
```
% git clone git@github.com:barryclark/jekyll-now.git
```

log
```
yamatokataoka@Yamatos-MacBook-Pro workspace % git clone git@github.com:barryclark/jekyll-now.git
Cloning into 'jekyll-now'...
remote: Enumerating objects: 1300, done.
remote: Total 1300 (delta 0), reused 0 (delta 0), pack-reused 1300
Receiving objects: 100% (1300/1300), 8.21 MiB | 1.97 MiB/s, done.
Resolving deltas: 100% (713/713), done.
yamatokataoka@Yamatos-MacBook-Pro workspace % cd jekyll-now
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % ls -l
total 72
-rw-r--r--  1 yamatokataoka  staff   348 Dec 24 20:34 404.md
-rw-r--r--  1 yamatokataoka  staff     1 Dec 24 20:34 CNAME
-rw-r--r--  1 yamatokataoka  staff  1077 Dec 24 20:34 LICENSE
-rw-r--r--  1 yamatokataoka  staff  7941 Dec 24 20:34 README.md
-rw-r--r--  1 yamatokataoka  staff  2540 Dec 24 20:34 _config.yml
drwxr-xr-x  6 yamatokataoka  staff   192 Dec 24 20:34 _includes
drwxr-xr-x  5 yamatokataoka  staff   160 Dec 24 20:34 _layouts
drwxr-xr-x  3 yamatokataoka  staff    96 Dec 24 20:34 _posts
drwxr-xr-x  6 yamatokataoka  staff   192 Dec 24 20:34 _sass
-rw-r--r--  1 yamatokataoka  staff   258 Dec 24 20:34 about.md
drwxr-xr-x  8 yamatokataoka  staff   256 Dec 24 20:34 images
-rw-r--r--  1 yamatokataoka  staff   368 Dec 24 20:34 index.html
-rw-r--r--  1 yamatokataoka  staff  3863 Dec 24 20:34 style.scss
```

To create a local repository with a clean commit history, remove .git folder.
```
% rm -rf .git
```

> rm - command to delete one or more files or directories  
> -rf - r means recursive removal, it is useful for deleting directory and f which a removal will continue without prompting you

now jekyll-now setting up has finished.

# 1 Set up Docker
## 1 Learn Docker concepts
Firstly read the [overview](https://docs.docker.com/engine/docker-overview/) to get basic understanding about docker.

And get started with [Orientation and setup](https://docs.docker.com/get-started/).

## 2 Install Docker
Follow [Install Docker Desktop on mac](https://docs.docker.com/docker-for-mac/install/).

## 3 Pull Jekyll image
Jekyll provides their own docker image pre-installed Jekyll.

run the Jekyll image on Docker from a new jekyll-now directory
```
% docker run --rm -it --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" jekyll/jekyll /bin/bash
```

If you're running this command for the first time, the image for this container won't be on your system, so it'll grab it from the Docker registry first before it runs the container.

> docker - base command for the Docker CLI  
>  
> run - When execute docker run, the container process that runs is isolated in that it has its own file system, its own networking, and its own isolated process tree separate from the host.  
>  
> –rm - option remove container after it exits (useful for short lived containers or commands)  
>  
> --volume="$PWD:/srv/jekyll" - option to take the current directory indicated by $PWD and map it to the directory at /srv/jekyll within the container  
>  
> --volume="$PWD/vendor/bundle:/usr/local/bundle" - option maps the contents of the current directory's /vendor/bundle and maps it to /usr/local/bundle. The reason for this option is so that gems could be cached and reused in future builds  
>  
> -it - interactive terminal so we can see output on the screen  
>  
> jekyll/jekyll:latest - this tells it to use the jekyll:3.8 tagged version of the [Jekyll container](https://github.com/envygeeks/jekyll-docker)  
>  
> /bin/bash - command we want to run ie go to bash  

log
```
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % docker run --rm -it --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" jekyll/jekyll /bin/bash
Unable to find image 'jekyll/jekyll:latest' locally
latest: Pulling from jekyll/jekyll
9d48c3bd43c5: Pull complete
9ce9598067e7: Pull complete
278f4c997324: Pull complete
867dd521f6d0: Pull complete
c69cba5b7867: Pull complete
828c8f2de574: Pull complete
Digest: sha256:d1bf33637d476e3cb2d5858038673cc93bc961e9390d31171d9febde5c5d24fd
Status: Downloaded newer image for jekyll/jekyll:latest
bash-5.0#
bash-5.0# exit
exit
yamatokataoka@Yamatos-MacBook-Pro jekyll-now %
```

## 4 Serve the site locally
run to serve a site locally using port 4000

A Jekyll blog is being generated and served from the Docker container and you can point your browser to localhost:4000 and see the Docker served site.
```
docker run --rm -it -p 4000:4000 --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" jekyll/jekyll /bin/bash jekyll serve --force_polling
```

> -p 4000:4000 - option to expose a container’s internal port 4000 and the exposed port is accessible on the host and the port 4000  
>  
> jekyll serve - runs the serve command for Jekyll  
>  
> --force_polling - option for Jekyll to force auto-regeneration of the site when files are modified.

see your site by going to localhost:4000 in your browser
![localhost]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-24 at 22.43.00.png)

# 3 Publish a blog on GitHub Pages
## 1 Create new GitHub repository
First create a remote repository on GitHub.
In the upper-right corner of any page, use the drop-down menu, and select New repository.

![new repository]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-21 at 15.03.48.png)

Select or put as the following in the picture below.

* Owner - the account you created previously

* Repository name - creating a user or organization site, your repository must be named <user>.github.io (In this guide, yamatokataoka.github.io)

* Public - Choose to make the repository either public or private. Public repositories are visible to the public, while private repositories are only accessible to you, and people you share them with. (In this guide, Public)

Click Create repository.

![new repository conf]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-21 at 16.02.59.png)

After creating new repository, you can see like following screenshot.

![new repository files]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-21 at 16.03.41.png)

## 2 Create new repository on the command line
Follow the instructions that show on GitHub repository home basically on the jekyll-now foloder, ~/workspace/jekyll-now.  

initialize a local Git repository.  
```
% git init
```

log
```
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % git init
Initialized empty Git repository in /Users/yamatokataoka/workspace/jekyll-now/.git/
```

Add all files (whcih indicates ".") to the repository staging area  
```
% git add .
```

log
```
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % git add .
yamatokataoka@Yamatos-MacBook-Pro jekyll-now %
```

Create a new commit with a message describing what work was done in the commit (In this case, "first commit")  
```
% git commit -m "first commit"
```
After executing above, your repo will now have all files which you created with jekyll new . command on Docker, added to the history and will track future updates to the files.  

<details>
<summary>log</summary>

<pre>
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % git commit -m "first commit"
[master (root-commit) 0bf4096] first commit
 32 files changed, 929 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 .jekyll-cache/Jekyll/Cache/Jekyll--Cache/b7/9606fb3afea5bd1609ed40b622142f1c98125abcfe89a76a661b0e8e343910
 create mode 100644 .jekyll-cache/Jekyll/Cache/Jekyll--Converters--Markdown/20/4cd43588fc3c9384bf4d82cfa2390cea42d2c957c5d595abce017b60ab5dae
 create mode 100644 .jekyll-cache/Jekyll/Cache/Jekyll--Converters--Markdown/2f/644b4d1157f7c45f8f31e73874d2c524849c7618b71e00470ee21043263b2a
 create mode 100644 .jekyll-cache/Jekyll/Cache/Jekyll--Converters--Markdown/ad/ec53e4f43e6bb7d97b2ff268bf8439495395f816120581ad7730b8d0ba6bb7
 create mode 100644 .jekyll-cache/Jekyll/Cache/Jekyll--Converters--Markdown/d8/9b23a2ca96e9a3e0b9e5254fe5e18b7396b29845010f5e813665eecebae45b
 create mode 100644 404.md
 create mode 100644 CNAME
 create mode 100644 LICENSE
 create mode 100644 README.md
 create mode 100644 _config.yml
 create mode 100644 _includes/analytics.html
 create mode 100644 _includes/disqus.html
 create mode 100644 _includes/meta.html
 create mode 100644 _includes/svg-icons.html
 create mode 100644 _layouts/default.html
 create mode 100644 _layouts/page.html
 create mode 100644 _layouts/post.html
 create mode 100644 _posts/2014-3-3-Hello-World.md
 create mode 100644 _sass/_highlights.scss
 create mode 100644 _sass/_reset.scss
 create mode 100644 _sass/_svg-icons.scss
 create mode 100644 _sass/_variables.scss
 create mode 100644 about.md
 create mode 100644 images/404.jpg
 create mode 100644 images/config.png
 create mode 100644 images/first-post.png
 create mode 100644 images/jekyll-logo.png
 create mode 100644 images/jekyll-now-theme-screenshot.jpg
 create mode 100644 images/step1.gif
 create mode 100644 index.html
 create mode 100644 style.scss
</pre>
</details>

Add your GitHub repository as a remote, replacing USER with the account that owns the repository and REPOSITORY with the name of the repository, it would be <user>.github.io.
```
% git remote add origin git@github.com:USER/REPOSITORY
```

log
```
yamatokataoka@Yamatos-MacBook-Pro blog % git remote add origin git@github.com:yamatokataoka/yamatokataoka.github.io.git
yamatokataoka@Yamatos-MacBook-Pro blog %
```

Push the repository to GitHub, replacing BRANCH with the name of the branch you're working on. (In this guide master)  
```
% git push -u origin BRANCH
```

log
```
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % git push -u origin master
Enumerating objects: 49, done.
Counting objects: 100% (49/49), done.
Delta compression using up to 4 threads
Compressing objects: 100% (45/45), done.
Writing objects: 100% (49/49), 1.17 MiB | 5.02 MiB/s, done.
Total 49 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), done.
To github.com:yamatokataoka/yamatokataoka.github.io.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
yamatokataoka@Yamatos-MacBook-Pro jekyll-now %
```

On GitHub, navigate to or reload your site's repository.  
Check all files are appered on GitHub repository page.  
![files on GitHub repo]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-25 at 19.46.27.png)

## 3 Publish your site on GitHub Pages
Your Jekyll blog will often be viewable immediately at https://USER.github.io.

![https://USER.github.io]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-25 at 19.52.02.png)

> Note: It can take up to 20 minutes for changes to your site to publish after you push the changes to GitHub. If your don't see your changes reflected in your browser after an hour  
