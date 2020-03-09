---
layout: post
title: Create a blog using Jekyll and GitHub pages with Docker
---

This is a complete guide for blog creating with Jekyll and Docker. Jekyll is a static site generator that you can use to create simple sites or blogs and Github pages is a static site hosting service.

With Docker, it could compile or even serve a Jekyll site locally without going through the entire fuss of getting Jekyll up and running on a local machine.

After setting up a basic Jekyll Now blog, this guide moves onto more advanced topic dealing with HTML, CSS and Jekyll configuration. You will be more confortable with Jekyll and designing your own blog.

# Prerequisites
- Mac
- A GitHub account

# Goal
This is what the website we make will look like:

![example website]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-24 at 19.21.02.png)

# Create a Jekyll blog
reference: [https://davemateer.com/2018/01/25/Jekyll-and-Docker](https://davemateer.com/2018/01/25/Jekyll-and-Docker)

## Learn Jekyll and Theme
[Jekyll](https://jekyllrb.com) is a website generator that’s designed for building minimal, static blogs to be hosted on GitHub Pages.

There are multiple ways to get started with Jekyll, each with its own variations. Here are a few options:

* Install Jekyll locally via the command line, create a new plane website using `jekyll new`, build it locally with `jekyll build`, and then serve it.

* Clone a repository as a starting point to your local machine, install Jekyll locally via the command line, make updates to your website, build it locally, and then serve it. (in this guide, Jekyll will be installed on docker)

In this guide, the theme, [Jekyll Now](http://www.github.com/barryclark/jekyll-now) will be used as a starting point.

## Learn Git, GitHub and GitHub Pages
[Git](https://git-scm.com) is the most widely used modern version control system in the world today.

[GitHub](https://github.com) is a Git repository hosting service, but it adds many of its own features. While Git is a command line tool, GitHub provides a Web-based graphical interface.

[GitHub Pages](https://pages.github.com) is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub, optionally runs the files through a build process, and publishes a website.

## Set up Git
Follow instructions on [Set up Git](https://help.github.com/en/github/getting-started-with-github/set-up-git#setting-up-git) on GitHub manual.  

## Set up GitHub account
Set up GitHub account with the [official guide](https://help.github.com/en/github/getting-started-with-github/signing-up-for-a-new-github-account).

## Clone a starting point
We’ll start by cloning the repository, Jekyll Now, that has followed best practices. This will get us on the right track and save a lot of time.

Open terminal on mac.

If you don't have workspace folder on your mac, create with `mkdir ~/workspace`.

> `mkdir ~/workspace` - command stands for makes the directory named workspace on ~/ which is home directory

<details>
<summary>log</summary>

<pre>
yamatokataoka@Yamatos-MacBook-Pro ~ % mkdir workspace
yamatokataoka@Yamatos-MacBook-Pro ~ %
yamatokataoka@Yamatos-MacBook-Pro ~ % ls -l
total 0
drwx------@  3 yamatokataoka  staff    96 Dec 21 12:44 Applications
drwxrwxrwx   5 yamatokataoka  staff   160 Apr 14  2019 Backup
drwx------+  5 yamatokataoka  staff   160 Dec 27 22:21 Desktop
drwx------+  4 yamatokataoka  staff   128 Sep 16 19:30 Documents
drwx------@ 16 yamatokataoka  staff   512 Dec 26 09:17 Downloads
# ... omitted
drwxr-xr-x   9 yamatokataoka  staff   288 Sep 23 14:15 share
drwxr-xr-x  14 yamatokataoka  staff   448 Dec 27 23:37 workspace
</pre>
</details>

Run below command in wherever you want (In this guide, `~/workspace`)

```
% git clone git@github.com:barryclark/jekyll-now.git
```

> `git clone` - git command to copy the repository on GitHub on your local computer

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

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

</details>

{::options parse_block_html="false" /}

now jekyll-now setting up has finished on your local.

# Set up Docker
## Learn Docker concepts
Firstly read the [overview](https://docs.docker.com/engine/docker-overview/) to get basic understanding about docker.

And get started with [Orientation and setup](https://docs.docker.com/get-started/).

## Install Docker
Follow [Install Docker Desktop on mac](https://docs.docker.com/docker-for-mac/install/).

## Pull Jekyll image
Jekyll provides their own docker image pre-installed Jekyll.

run the Jekyll image on Docker from a new jekyll-now directory

```
% docker run --rm -it --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" jekyll/jekyll /bin/bash
```

If you're running this command for the first time, the image for this container won't be on your system, so it'll grab it from the Docker registry first before it runs the container.

> `docker` - base command for the Docker CLI  
>  
> `run` - When execute docker run, the container process that runs is isolated in that it has its own file system, its own networking, and its own isolated process tree separate from the host.  
>  
> `–rm` - option remove container after it exits (useful for short lived containers or commands)  
>  
> `--volume="$PWD:/srv/jekyll"` - option to take the current directory indicated by $PWD and map it to the directory at /srv/jekyll within the container  
>  
> `--volume="$PWD/vendor/bundle:/usr/local/bundle"` - option maps the contents of the current directory's /vendor/bundle and maps it to /usr/local/bundle. The reason for this option is so that gems could be cached and reused in future builds  
>  
> `-it` - interactive terminal so we can see output on the screen  
>  
> `jekyll/jekyll:latest` - this tells it to use the jekyll:3.8 tagged version of the [Jekyll container](https://github.com/envygeeks/jekyll-docker)  
>  
> `/bin/bash` - command we want to run ie go to bash  

<details>
<summary>log</summary>

<pre>
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
</pre>
</details>

## Serve the site locally
run to serve a site locally using port 4000

A Jekyll blog is being generated and served from the Docker container and you can point your browser to `localhost:4000` and see the Docker served site.

```
docker run --rm -it -p 4000:4000 --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" jekyll/jekyll /bin/bash jekyll serve --force_polling
```

> `-p 4000:4000` - option to expose a container’s internal port 4000 and the exposed port is accessible on the host and the port 4000  
>  
> `jekyll serve` - runs the serve command for Jekyll  
>  
> `--force_polling` - option for Jekyll to force auto-regeneration of the site when files are modified.

see your site by going to `localhost:4000` in your browser
{% include helpers/image.html name="Screen Shot 2019-12-24 at 22.43.00.png" %}

# Publish a blog on GitHub Pages
## Create new GitHub repository
First create a remote repository on GitHub.

In the upper-right corner of any page, use the drop-down menu, and select New repository.

{% include helpers/image.html name="Screen Shot 2019-12-21 at 15.03.48.png" %}

Select or put as the following in the picture below.

* Owner - the account you created previously

* Repository name - creating a user or organization site, your repository must be named <user>.github.io (In this guide, yamatokataoka.github.io)

* Public - Choose to make the repository either public or private. Public repositories are visible to the public, while private repositories are only accessible to you, and people you share them with. (In this guide, Public)

Click Create repository.

{% include helpers/image.html name="Screen Shot 2019-12-21 at 16.02.59.png" %}

After creating new repository, you can see like following screenshot.

{% include helpers/image.html name="Screen Shot 2019-12-21 at 16.03.41.png" %}

## Create new repository on the command line
Follow the instructions on the jekyll-now foloder, `~/workspace/jekyll-now` in this guide.

To create a local repository with a clean commit history, remove `.git` folder on the jekyll-now repository.

```
% rm -rf .git
```

> `rm` - command to delete one or more files or directories  
>  
> `-rf` - r means recursive removal, it is useful for deleting directory and f which a removal will continue without prompting you

<details>
<summary>log</summary>

<pre>
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % rm -rf .git
yamatokataoka@Yamatos-MacBook-Pro jekyll-now %
</pre>
</details>

initialize a local Git repository.

```
% git init
```

<details>
<summary>log</summary>

<pre>
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % git init
Initialized empty Git repository in /Users/yamatokataoka/workspace/jekyll-now/.git/
</pre>
</details>

Add all files (whcih indicates ".") to the repository staging area

```
% git add .
```

<details>
<summary>log</summary>

<pre>
yamatokataoka@Yamatos-MacBook-Pro jekyll-now % git add .
yamatokataoka@Yamatos-MacBook-Pro jekyll-now %
</pre>
</details>

Create a new commit with a message describing what work was done in the commit (In this case, "first commit")

```
% git commit -m "first commit"
```

After executing above, your repo will now have all files which you created with jekyll new . command on Docker, added to the history and will track future updates to the files.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">log</summary>

```
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
```

</details>

{::options parse_block_html="false" /}

Add your GitHub repository as a remote, replacing `USER` with the account that owns the repository and `REPOSITORY` with the name of the repository, it would be `<user>.github.io`.

```
% git remote add origin git@github.com:USER/REPOSITORY
```

<details>
<summary>log</summary>

<pre>
yamatokataoka@Yamatos-MacBook-Pro blog % git remote add origin git@github.com:yamatokataoka/yamatokataoka.github.io.git
yamatokataoka@Yamatos-MacBook-Pro blog %
</pre>
</details>

Push the repository to GitHub, replacing BRANCH with the name of the branch you're working on. (In this guide, master)

```
% git push -u origin BRANCH
```

<details>
<summary>log</summary>

<pre>
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
</pre>
</details>

On GitHub, navigate to or reload your site's repository.

Check all files are appered on GitHub repository page.

{% include helpers/image.html name="Screen Shot 2019-12-25 at 19.46.27.png" %}

## Publish your site on GitHub Pages
Your Jekyll blog will often be viewable immediately at https://USER.github.io.

{% include helpers/image.html name="Screen Shot 2019-12-25 at 19.52.02.png" %}

> Note: It can take up to 20 minutes for changes to your site to publish after you push the changes to GitHub. If your don't see your changes reflected in your browser after an hour  

# Customize and view your site (Ongoing)
This is example configurating for Jeyll Now.

## Edit \_config.yml file
Enter your site name, description, avatar and many other options by editing the `_config.yml` file. You can easily turn on Google Analytics tracking, Disqus commenting and social icons here too.

comments below all set up will help you configurating.

My final configuration looks like this:

{::options parse_block_html="true" /}

<details>
<summary markdown="span">\_config.yml</summary>

```
#
# This file contains configuration flags to customize your site
#

# Name of your site (displayed in the header)
name: Yamato Kataoka

# Short bio or description (displayed in the header)
description: Software Engineer

# URL of your avatar or profile pic (you could use your GitHub profile pic)
avatar: /images/profile.png

#
# Flags below are optional
#

# Includes an icon in the footer for each username you enter
footer-links:
  dribbble:
  email:
  facebook:
  flickr:
  github: yamatokataoka
  instagram:
  linkedin:
  pinterest:
  rss: # just type anything here for a working RSS icon
  twitter:
  stackoverflow: # your stackoverflow profile, e.g. "users/50476/bart-kiers"
  youtube: # channel/&lt;your_long_string> or user/&lt;user-name>
  googleplus: # anything in your profile username that comes after plus.google.com/


# Enter your Disqus shortname (not your username) to enable commenting on posts
# You can find your shortname on the Settings page of your Disqus account
disqus:

# Enter your Google Analytics web tracking code (e.g. UA-2110908-2) to activate tracking
google_analytics:

# Your website URL (e.g. http://barryclark.github.io or http://www.barryclark.co)
# Used for Sitemap.xml and your RSS feed
url: https://yamatokataoka.github.io

# If you're hosting your site at a Project repository on GitHub pages
# (http://yourusername.github.io/repository-name)
# and NOT your User repository (http://yourusername.github.io)
# then add in the baseurl here, like this: "/repository-name"
baseurl: ""

#
# !! You don't need to change any of the configuration flags below !!
#

permalink: /:title/

# The release of Jekyll Now that you're using
version: v1.2.0

# Jekyll 3 now only supports Kramdown for Markdown
kramdown:
  # Use GitHub flavored markdown, including triple backtick fenced code blocks
  input: GFM
  # Jekyll 3 and GitHub Pages now only support rouge for syntax highlighting
  syntax_highlighter: rouge
  syntax_highlighter_opts:
    # Use existing pygments syntax highlighting css
    css_class: 'highlight'

# Set the Sass partials directory, as we're using @imports
sass:
  style: :expanded # You might prefer to minify using :compressed

# Use the following plug-ins
gems:
  - jekyll-sitemap # Create a sitemap using the official Jekyll sitemap gem
  - jekyll-feed # Create an Atom feed using the official Jekyll feed gem

# Exclude these files from your production _site
exclude:
  - Gemfile
  - Gemfile.lock
  - LICENSE
  - README.md
  - CNAME
  - vendor
  - .jekyll-cache
  - .gitignore
```

> `avatar: /images/profile.png` - here you can specify the location of image like `/images/profile.png`
>
> `baseurl: ""` -  `baseurl` will be blank for User repository.

</details>

{::options parse_block_html="false" /}

## Fix highlight scss
Replace .highlight to pre on `jekyll-now/_sass/_highlights.scss` for fixing bug on Jekyll Now. This bug is reported on the original repository as a [issue](https://github.com/barryclark/jekyll-now/issues/1526).

```
# ... omitted
 pre {
   background-color: #efefef;
   padding: 7px 7px 7px 10px;
   border: 1px solid #ddd;
# ... omitted
```

## Update highlight scss
To change github-like code block, Update `_sass/_highlights.scss` provides styling of highlight block.

{::options parse_block_html="true" /}

<details>
<summary markdown="span">\_sass/\_highlights.scss</summary>

```
pre {
  background-color: #efefef;
  padding: 16px;
  margin: 20px 0 20px 0;
  overflow: auto;
  border-radius: 3px;
}

code {
  background-color: #efefef;
  font-family:'Bitstream Vera Sans Mono','Courier', monospace;
  border-radius: 3px;
}
# ...omitted (the same with original)
```

</details>

{::options parse_block_html="false" /}


## Update home layout
Configure to make the navigation bar on the top of a page.

Deleted below css of .container block on syle.scss

```
   margin: 0 auto;
   max-width: 740px;
```

You can try out on your browser with Inspect Element.

![Inspect Element]({{ site.baseurl }}/images/posts/2019-12-22-create-a-blog-using-jekyll-and-github-pages-with-docker/Screen Shot 2019-12-25 at 20.50.18.png)

after edtting, it looks like this.

```
# ...omitted
.container {
   padding: 0 10px;
   width: 100%;
 }
# ...omitted
```

and add new lines as follows for applying full browser width to only the nav bar.

```
# ...omitted
#main.container {
   margin: 0 auto;
   max-width: 740px;
 }
# ...omitted
```

also delete font size specification on blockquote block inside .post.

```
# ...omitted
.post {
  blockquote {
    margin: 1.8em .8em;
     border-left: 2px solid $gray;
     padding: 0.1em 1em;
     color: $gray;
     font-size: 22px;
     font-style: italic;
   }
# ...omitted
```

the final layout looks like this:

{% include helpers/image.html name="Screen Shot 2019-12-29 at 18.15.38.png" %}

## Add details tag style

There is no style on HTML5 `details` tag.

Add style under `_sass/` named like `_details.scss`

```
details {
  padding: 1em;
  border: 1px solid #e6e6e6;
  border-radius: 5px;
}
```

Add add import statement on the scss file for `_details.scss`.

```
---
---

//
// IMPORTS
//

@import "reset";
@import "variables";
@import "details";
# omitted ...
```

Reference: [The Details and Summary HTML Elements](https://alligator.io/html/details-summary-elements/)

# Set up Docker Compose (future)
