+++
title = "Hugo from zero to hero"
date = "2026-07-27T22:33:44+02:00"
description = "Bulding and deploying a personal Hugo blog."
tags = ["hugo","blogging","hugo-themes","hextra",]
+++

This is the meta-post. The post about how to build your own blog. I will use [Hugo](https://gohugo.io/) and a Linux machine.

## Prerequisites
We need:
- Git
- Hugo

### Install git
Verify if `git` is installed. 
~~~
git --version
~~~

If the command is not found, [install it](https://git-scm.com/install/linux).

I am using Debian, so I'll run:
~~~
apt-get install git
add-apt-repository ppa:git-core/ppa
apt update; apt install git
~~~

### Install Hugo
Verify if `Hugo` is installed. I am using `v0.164`.
~~~
hugo version
~~~

If the command is not found, [install it](https://gohugo.io/installation/linux/).

I am using Debian, so I'll download [this file](https://github.com/gohugoio/hugo/releases/download/v0.164.0/hugo_0.164.0_linux-amd64.deb) and run:
~~~
sudo dpkg -i ~/Downloads/hugo_0.164.0_linux-amd64.deb
~~~

## Create a GitHub repository
This post is not just about creating a local blog, but also hosting it and having it published for everyone to see. For that, we will be using GitHub Pages.

If you don't already have a [GitHub](https://github.com/) account, create it. 

Create a [new repository](https://github.com/new) and name it like this: `<your_username>.github.io`. This specific naming will tell GitHub that this repository will be deployed and published.

You can add your own description. I didn't add a README and I chose GNU's license. The repo needs to be public.

Hit create, now you have your new repository for your blog. [This](https://github.com/mikamp116/mikamp116.github.io) is mine.

Now you need to get your repository URL, click on `Code`and copy the Clone URL, which should look like `https://github.com/<your_username>/<your_username>.github.io.git`.

Open a terminal in your PC (hopefully you are using Linux) and create a directory where the repository will be cloned.
~~~
git clone <YOUR_CLONE_URL>
~~~

Now change your directory to the repository
~~~
cd <your_username>.github.io`
~~~

Hugo won't let you create a project in a directory that is not empty, so we will create a new project in a subdirectory and then move it back
~~~
hugo new project test
cp -r test .
rm -rf test
~~~

We can add a theme now, but we will leave it for later.

You can create a new page with
~~~
hugo new content <PATH>/<FILENAME>.md
~~~
By default all new content gets created as a draft, so don't forget to change that. 

Or copy the content from [this repo](https://github.com/janraasch/hugo-bearblog/tree/master/exampleSite/content) to get started faster.

Now run the server and click on the URL from the command output
~~~
hugo server
~~~
We will need the deployment script for the GitHub Action. [\[1\]][1]

Create a workflow file
~~~
mkdir .github/workflows
editor .github/workflows/hugo.yaml
~~~
And copy the content from [here](https://gohugo.io/host-and-deploy/host-on-github-pages/#step-2).

Next, add the following snippet to the hugo.toml file in the site root directory

You can customise now the content, or leave as it is for now, and then can commit and push the changes to your repository
~~~
git add .
git commit -m "My first personal blog"
git push
~~~

GitHub will run the workflow and publish the page


[1]:  https://gohugo.io/host-and-deploy/host-on-github-pages/#step-2
