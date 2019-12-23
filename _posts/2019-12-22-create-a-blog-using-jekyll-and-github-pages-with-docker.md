---
layout: post
title: Create a blog using Jekyll and GitHub pages with Docker
---

In this post, Jekyll is a static site generator that you can use to create simple sites or blogs and Github pages is a static site hosting service. With Docker, it could compile or even serve a Jekyll site locally without going through the entire fuss of getting Jekyll up and running on a local machine.

# Prerequisites
- mac
- A GitHub account

# Goal
This is what the website we make will look like:  
[picture]    
- example: this website

# 1 Set up Docker
## 1 Learn Docker concepts
Firstly read the [overview](https://docs.docker.com/engine/docker-overview/) to get basic understanding about docker.  
And get started with [Orientation and setup](https://docs.docker.com/get-started/).  

## 2 Install Docker
Follow [Install Docker Desktop on mac](https://docs.docker.com/docker-for-mac/install/).  

# 2 Create a Jekyll blog
reference: [https://davemateer.com/2018/01/25/Jekyll-and-Docker](https://davemateer.com/2018/01/25/Jekyll-and-Docker)
## 1 Learn Jekyll
[Jekyll](https://jekyllrb.com) is a website generator that’s designed for building minimal, static blogs to be hosted on GitHub Pages.  

## 2 Pull Jekyll image
open terminal on mac
create a directory for workspace of Jekyll blog.
```
% mkdir -p ~/workspace/blog
```

> mkdir - command to create new directory  
> -p - option to create sub-directories of a directory  
> ~/workspace/blog - directory path for Jekyll blog  

log
```
yamatokataoka@Yamatos-MacBook-Pro ~ % mkdir -p ~/workspace/blog
yamatokataoka@Yamatos-MacBook-Pro ~ %
```

check directory created
```
% cd ~/workspace/blog
% ls -l
```

> cd - command to change directory  
> ls - command to list directory contents of files and directories  
> -l - option to list out files and directories in long list format  

log
```
yamatokataoka@Yamatos-MacBook-Pro ~ % cd ~/workspace/blog
yamatokataoka@Yamatos-MacBook-Pro blog % ls -l
yamatokataoka@Yamatos-MacBook-Pro blog % 
```

run the Jekyll image on Docker from a new blog directory  
```
% docker run --rm -it --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" jekyll/jekyll /bin/bash
```

If you're running this command for the first time, the image for this container won't be on your system, so it'll grab it from the Docker registry first before it runs the container.

> docker - base command for the Docker CLI  
> run - When execute docker run, the container process that runs is isolated in that it has its own file system, its own networking, and its own isolated process tree separate from the host.  
> –rm - option remove container after it exits (useful for short lived containers or commands)  
> --volume="$PWD:/srv/jekyll" - option to take the current directory indicated by $PWD and map it to the directory at /srv/jekyll within the container    
> --volume="$PWD/vendor/bundle:/usr/local/bundle" - option maps the contents of the current directory's /vendor/bundle and maps it to /usr/local/bundle. The reason for this option is so that gems could be cached and reused in future builds
> -it - interactive terminal so we can see output on the screen  
> jekyll/jekyll:latest - this tells it to use the jekyll:3.8 tagged version of the [Jekyll container](https://github.com/envygeeks/jekyll-docker)  
> /bin/bash - command we want to run ie go to bash  

log
```
yamatokataoka@Yamatos-MacBook-Pro blog % docker run --rm -it --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" jekyll/jekyll /bin/bash
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
```

## 3 Create a brand new blog
run command inside a docker:
```
# jekyll new .
```

<details>
<summary>log</summary>

<pre>
bash-5.0# jekyll new .
ruby 2.6.5p114 (2019-10-01 revision 67812) [x86_64-linux-musl]
Running bundle install in /srv/jekyll... 
  Bundler: Fetching gem metadata from https://rubygems.org/...........
  Bundler: Fetching gem metadata from https://rubygems.org/.
  Bundler: Resolving dependencies...
  Bundler: Fetching public_suffix 4.0.1
  Bundler: Installing public_suffix 4.0.1
  Bundler: Fetching addressable 2.7.0
  Bundler: Installing addressable 2.7.0
  Bundler: Using bundler 2.0.2
  Bundler: Fetching colorator 1.1.0
  Bundler: Installing colorator 1.1.0
  Bundler: Fetching concurrent-ruby 1.1.5
  Bundler: Installing concurrent-ruby 1.1.5
  Bundler: Fetching eventmachine 1.2.7
  Bundler: Installing eventmachine 1.2.7 with native extensions
  Bundler: Fetching http_parser.rb 0.6.0
  Bundler: Installing http_parser.rb 0.6.0 with native extensions
  Bundler: Fetching em-websocket 0.5.1
  Bundler: Installing em-websocket 0.5.1
  Bundler: Fetching ffi 1.11.3
  Bundler: Installing ffi 1.11.3 with native extensions
  Bundler: Fetching forwardable-extended 2.6.0
  Bundler: Installing forwardable-extended 2.6.0
  Bundler: Fetching i18n 1.7.0
  Bundler: Installing i18n 1.7.0
  Bundler: Fetching sassc 2.2.1
  Bundler: Installing sassc 2.2.1 with native extensions
  Bundler: Fetching jekyll-sass-converter 2.0.1
  Bundler: Installing jekyll-sass-converter 2.0.1
  Bundler: Fetching rb-fsevent 0.10.3
  Bundler: Installing rb-fsevent 0.10.3
  Bundler: Fetching rb-inotify 0.10.0
  Bundler: Installing rb-inotify 0.10.0
  Bundler: Fetching listen 3.2.1
  Bundler: Installing listen 3.2.1
  Bundler: Fetching jekyll-watch 2.2.1
  Bundler: Installing jekyll-watch 2.2.1
  Bundler: Fetching kramdown 2.1.0
  Bundler: Installing kramdown 2.1.0
  Bundler: Fetching kramdown-parser-gfm 1.1.0
  Bundler: Installing kramdown-parser-gfm 1.1.0
  Bundler: Fetching liquid 4.0.3
  Bundler: Installing liquid 4.0.3
  Bundler: Fetching mercenary 0.3.6
  Bundler: Installing mercenary 0.3.6
  Bundler: Fetching pathutil 0.16.2
  Bundler: Installing pathutil 0.16.2
  Bundler: Fetching rouge 3.14.0
  Bundler: Installing rouge 3.14.0
  Bundler: Fetching safe_yaml 1.0.5
  Bundler: Installing safe_yaml 1.0.5
  Bundler: Fetching unicode-display_width 1.6.0
  Bundler: Installing unicode-display_width 1.6.0
  Bundler: Fetching terminal-table 1.8.0
  Bundler: Installing terminal-table 1.8.0
  Bundler: Fetching jekyll 4.0.0
  Bundler: Installing jekyll 4.0.0
  Bundler: Fetching jekyll-feed 0.13.0
  Bundler: Installing jekyll-feed 0.13.0
  Bundler: Fetching jekyll-seo-tag 2.6.1
  Bundler: Installing jekyll-seo-tag 2.6.1
  Bundler: Fetching minima 2.5.1
  Bundler: Installing minima 2.5.1
  Bundler: Bundle complete! 6 Gemfile dependencies, 30 gems now installed.
  Bundler: Bundled gems are installed into `/usr/local/bundle`
  Bundler: Post-install message from i18n:
  Bundler: 
  Bundler: HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
  Bundler: But that may break your application.
  Bundler: 
  Bundler: Please check your Rails app for 'config.i18n.fallbacks = true'.
  Bundler: If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
  Bundler: 'config.i18n.fallbacks = [I18n.default_locale]'.
  Bundler: If not, fallbacks will be broken in your app by I18n 1.1.x.
  Bundler: 
  Bundler: For more info see:
  Bundler: https://github.com/svenfuchs/i18n/releases/tag/v1.1.0
  Bundler: 
  Bundler: Post-install message from jekyll:
  Bundler: -------------------------------------------------------------------------------------
  Bundler: Jekyll 4.0 comes with some major changes, notably:
  Bundler: 
{% raw %}
  Bundler: * Our `link` tag now comes with the `relative_url` filter incorporated into it.
  Bundler: You should no longer prepend `{{ site.baseurl }}` to `{% link foo.md %}`
  Bundler: For further details: https://github.com/jekyll/jekyll/pull/6727
  Bundler: 
  Bundler: * Our `post_url` tag now comes with the `relative_url` filter incorporated into it.
  Bundler: You shouldn't prepend `{{ site.baseurl }}` to `{% post_url 2019-03-27-hello %}`
  Bundler: For further details: https://github.com/jekyll/jekyll/pull/7589
  Bundler: 
  Bundler: * Support for deprecated configuration options has been removed. We will no longer
  Bundler: output a warning and gracefully assign their values to the newer counterparts
  Bundler: internally.
  Bundler: -------------------------------------------------------------------------------------
{% endraw %}
New jekyll site installed in /srv/jekyll. 
</pre>
</details>

now exit out of bash and check a brand new Jekyll site on ~/workspace/blog

create new tab on a tarminal and run
```
# exit
% ls -l
```

log
```
bash-5.0# exit
exit
yamatokataoka@Yamatos-MacBook-Pro blog % ls -l
total 48
-rw-r--r--  1 yamatokataoka  staff   419 Dec 15 16:05 404.html
-rw-r--r--  1 yamatokataoka  staff  1126 Dec 15 16:05 Gemfile
-rw-r--r--  1 yamatokataoka  staff  1971 Dec 15 16:13 Gemfile.lock
-rw-r--r--  1 yamatokataoka  staff  2080 Dec 15 16:05 _config.yml
drwxr-xr-x  3 yamatokataoka  staff    96 Dec 15 16:05 _posts
-rw-r--r--  1 yamatokataoka  staff   539 Dec 15 16:05 about.markdown
-rw-r--r--  1 yamatokataoka  staff   175 Dec 15 16:05 index.markdown
drwxr-xr-x  3 yamatokataoka  staff    96 Dec 15 16:56 vendor
```

## 4 Serve the site locally
run to serve a site locally using port 4000

A Jekyll blog is being generated and served from the Docker container and you can point your browser to localhost:4000 and see the Docker served site.
```
docker run --rm -it -p 4000:4000 --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" jekyll/jekyll /bin/bash jekyll serve --force_polling
```

> -p 4000:4000 - option to expose a container’s internal port 4000 and the exposed port is accessible on the host and the port 4000  
> jekyll serve - runs the serve command for Jekyll  
> --force_polling - option for Jekyll to force auto-regeneration of the site when files are modified.

see your site by going to localhost:4000 in your browser
[your site]  

# 3 Publish a blog on GitHub Pages
## 1 Learn Git, GitHub and GitHub Pages
[Git](https://git-scm.com) is the most widely used modern version control system in the world today.

[GitHub](https://github.com) is a Git repository hosting service, but it adds many of its own features. While Git is a command line tool, GitHub provides a Web-based graphical interface.

[GitHub Pages](https://pages.github.com) is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub, optionally runs the files through a build process, and publishes a website.

## 2 Set up Git
Follow instructions on [Set up Git](https://help.github.com/en/github/getting-started-with-github/set-up-git#setting-up-git) on GitHub manual.  

## 3 Set up GitHub account
Set up GitHub account with the [official guide](https://help.github.com/en/github/getting-started-with-github/signing-up-for-a-new-github-account).

## 4 Create a repository for your site
### 1 In the upper-right corner of any page, use the  drop-down menu, and select New repository.
Select or put as the following in the picture
> Owner - the account you created previously   
> Repository name - creating a user or organization site, your repository must be named <user>.github.io (In this guide, yamatokataoka.github.io)  
> Public - Choose to make the repository either public or private. Public repositories are visible to the public, while private repositories are only accessible to you, and people you share them with. (In this guide, Public)  
[picture]

Click Create repository.  
### 2 Create a new repository on the command line
Follow the instructions that show on GitHub repository home basically on the blog foloder, ~/workspace/blog.  
Add README.md on your blog folder using describes your repository.  
```
echo "# blog" >> README.md
```
initialize a local Git repository.  
```
git init
```

Add all files (whcih indicates ".") to the repository staging area  
```
git add .
```

Create a new commit with a message describing what work was done in the commit (In this case, "first commit")  
```
git commit -m "first commit"
```
After executing above, your repo will now have all files which you created with jekyll new . command on Docker, added to the history and will track future updates to the files.  

Add your GitHub repository as a remote, replacing USER with the account that owns the repository and REPOSITORY with the name of the repository.  
```
git remote add origin git@github.com:USER/REPOSITORY
```

Push the repository to GitHub, replacing BRANCH with the name of the branch you're working on. (In this guide master)  
```
git push -u origin BRANCH
```

<details>
<summary>log</summary>

<pre>
yamatokataoka@Yamatos-MacBook-Pro blog % echo "# blog" >> README.md
yamatokataoka@Yamatos-MacBook-Pro blog % git init
Initialized empty Git repository in /Users/yamatokataoka/workspace/blog/.git/
yamatokataoka@Yamatos-MacBook-Pro blog % git add .
yamatokataoka@Yamatos-MacBook-Pro blog % git commit -m "first commit"
[master (root-commit) c921c57] first commit
 9 files changed, 253 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 404.html
 create mode 100644 Gemfile
 create mode 100644 Gemfile.lock
 create mode 100644 README.md
 create mode 100644 _config.yml
 create mode 100644 _posts/2019-12-15-welcome-to-jekyll.markdown
 create mode 100644 about.markdown
 create mode 100644 index.markdown
yamatokataoka@Yamatos-MacBook-Pro blog % git remote add origin git@github.com:yamatokataoka/yamatokataoka.github.io.git
yamatokataoka@Yamatos-MacBook-Pro blog % git push -u origin master
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 4 threads
Compressing objects: 100% (11/11), done.
Writing objects: 100% (12/12), 4.40 KiB | 2.20 MiB/s, done.
Total 12 (delta 0), reused 0 (delta 0)
To github.com:yamatokataoka/yamatokataoka.github.io.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
</pre>
</details>

On GitHub, navigate to your site's repository.  
Check all files are appered on GitHub repository page.  
[picture]

### 3 Publish your site on GitHub Pages
Under your repository name, click Settings.  
[picture]

To see your published site, under "GitHub Pages", click your site's URL.  
[picture]

> Note: It can take up to 20 minutes for changes to your site to publish after you push the changes to GitHub. If your don't see your changes reflected in your browser after an hour  

[picture]

# 4 Set up Docker Compose (future)
