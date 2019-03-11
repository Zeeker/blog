---
title: "How to build your professional website (like this one!)"
slug: how-to-build-your-professional-website
date: 2019-02-24T20:50:07+01:00
categories:
- tech
- web
tags:
- website
- hugo
- zeit
- now
- docker
keywords:
- tech
autoThumbnailImage: false
coverImage: cover.jpg
coverCaption: Photo by Christopher Gower on Unsplash
# coverSize: partial
# metaAlignment: center
---

<!-- So, you want to create your own website/blog/whatever. -->
<!-- Where do you start? -->
<!-- If you're like me, the idea of creating your own website/blog/whatever is intimidating. -->
The idea of creating your own website/blog/whatever can sound intimidating.
<!-- There are a million questions which need to be answered: -->
There are a million questions with seemingly even more answers.

- What's the best way to create your page?
<!-- From scatch? -->
<!-- A framework? -->
<!-- Some kind of editor? -->
<!-- Should you create it from scratch or use some kind of framework? -->
- Where can you host it?
- How do you get your own domain?

And many, many more.
Where do you even start?
<!--more-->

<!-- I certainly thought like that. -->
<!-- Luckily for you, I already did the hard work and then wrote this blog post. -->
<!-- Well, today is your lucky day. -->
But, you're in luck!
I used to have the same questions and today I'm gonna share my answers with you.
<!-- I obviously managed to do this, you're on my blog after all. -->
<!-- And if I can do it, you can too. -->
So please, sit back, grab a hot beverage and enjoy the hard earned knowledge I distilled in this blog post.

<!--toc-->

# What you will learn

In this post you will learn how to:

- easily create your site using [hugo][hugo]
- deploy and host your page with [now][now]
- setup your own domain
- use [github][github] to automatically deploy everything on push

At the end of this you'll have all the skills necessary to create a website **just like this one**.

*Note: This post assumes you have some basic knowledge about the command line and git.*
*If you are not familiar with git - or don't feel comfortable using it - [take a look at it's website](https://git-scm.com/).*

# Create your page using [hugo][hugo]

Hugo claims to be "the world’s fastest framework for building websites".
I have no idea if that's true but I can say that it's easy to setup, use, and produces great results.
<!-- But I'm getting ahead of myself. -->
In this section we will pretty much follow along [hugo's quickstart](https://gohugo.io/getting-started/quick-start/).
So if you would rather read that, go ahead.
No hard feelings.

Assuming you're on macOS installing hugo is as simple as typing into your CLI (you'll need to have [brew](https://brew.sh/) installed):

```sh
brew install hugo
```

*[Click here to find out how to install hugo for other platforms.](https://gohugo.io/getting-started/installing)*

<!-- After that you can create the basic framework of your future site by typing: -->
After that you can create your future site by typing:

```sh
hugo new site awesome-future-site
```

<!-- This will create a folder called (you might have guessed it) `awesome-future-site`. -->
This will create a folder named - you might have guessed it - `awesome-future-site`.
<!-- You could now use `hugo server` to see how it looks, but **spoiler** that would be pretty boring. -->
You could now use `hugo server` to see how it looks, but (**spoiler**) it's pretty boring.
By default hugo generates an empty page with nothing in it.
So how do we make it pretty?

This is where themes come into play.

## Picking a theme

Hugo offers a number of themes, most of them contributed by the community.
In this tutorial I'll go with the [tranquilpeak theme](https://themes.gohugo.io/hugo-tranquilpeak-theme/) simply because it's the one you're looking at right now.
Feel free to look through [the other ones hugo is offering](https://themes.gohugo.io/).

{{<
  figure
    caption="The Tranquilpeak Theme"
    src="tranquilpeak.png"
    link="https://themes.gohugo.io/hugo-tranquilpeak-theme/"
    target="_blank"
>}}

To install a theme you'll need to download it into the `themes` folder of your `awesome-future-site`.
How do you do that?
Going by hugo's quickstart you should use `git` - this is also what I would suggest.

```sh
cd awesome-future-site

git init
git submodule add https://github.com/kakawait/hugo-tranquilpeak-theme.git themes/hugo-tranquilpeak-theme
```

In case the `git submodule` part doesn't make sense to you: it's basically a way of telling get to keep track of a "sub project".
Don't worry too much about it.
If you want to worry you can read more about it [here](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

Okay, now we have the theme downloaded but how do we use it?
Great question!

```sh
echo 'theme = "hugo-tranquilpeak-theme"' >> config.toml
```

This appends the line `theme = "hugo-tranquilpeak-theme"` to your `config.toml` file.
Alternatively you can just open it with your favorite editor and add it this way.

Let's look at your page again, shall we?
Reminder: use `hugo server` to render the page.

{{<
  image
    classes="fancybox"
    src="page-with-theme.png"
>}}

Meh, still rather boring but we're getting there!

Lucky for us tranquilpeak offers an example configuration which allows us to bootstrap the whole process.

```sh
# Backup your previous configuraiton, if you want
cp config.toml config.toml.backup
cp themes/hugo-tranquilpeak-theme/exampleSite/config.toml .
```

<!-- How does it look like now (as a reminder, type `hugo server` into your command line)? -->
How does it look like now? 

{{<
  image
    alt="Your new page with some configuration"
    classes="fancybox"
    src="page-with-configured-theme.png"
 >}}

Now that's something!

<!-- From here on it should be easy to look into the `config.toml`  -->
<!-- Feel free to play a bit around with the `config.toml` and look how it affects the page. -->
Go ahead, play a bit around with the various options in the `config.toml` and see how it affects the page.
I'll wait here for you.

Also checkout [tranquilpeak's user documentation](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md) to see which configuration does what.
Alternatively you can look at [my configuration on github](https://github.com/Zeeker/blog/blob/post/how-to-build-your-professional-website/config.yml).

## Content, content, content

Now that we have the basic scaffolding for your page it's time to start writing.
With hugo this is done in [markdown][markdown].
If you're unfamiliar with markdown I would suggest to google for a tutorial, it's really simple and great to use.

With that out of the way, lets create your first post!
Open your command line again and type:

```sh
hugo new post/my-first-post.md
```

This will create a file at `content/post/my-first-post.md` which should roughly look like this:

```markdown
---
title: "My First Post"
date: 2019-03-08T23:45:06+01:00
categories:
- category
- subcategory
tags:
- tag1
- tag2
keywords:
- tech
#thumbnailImage: //example.com/image.jpg
---


```

<!-- ;;; Write more here! -->

You can now start typing away merrily and check your progress with `hugo server`.
To get an impression how a finished post might look like you can checkout [the markdown for this very post!](https://github.com/Zeeker/blog/blob/master/content/post/how-to-build-your-professional-website/index.md)

Also you might want to take a peek into the [relevant section in the tranquilpeak docs](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md#writing-posts), which explains all the configuration seen above.

We could continue to talk about all the features of hugo but that would blow this post out of proportion.
There are more interesting things to come.

## And now?

<!-- Before we go on to the next section (hosting) let's quickly recap what we learned. -->
Let's recap.
We've learned how to create a basic page with hugo and how to write simple posts with it.
<!-- REPHRASE -->
But up until now everything was just locally.

The real question is: How do we get this on the web?
Enter "now".

# Hosting made simple: now by zeit

[now][now] is a deployment and hosting service by the fine folks at zeit.
It's mainly target at serverless applications but can just as easily be used for website hosting.

This section will teach you a number of things:

1. how to use `now` to immediately put your page onto the web
2. how to build your page with `now`
3. how to automate the whole process

<!-- Step 2 will then allow us to automate the whole process, so you just need to push your changes to github. -->
At the end of it you'll have a repository up on github and your page will be automagically deployed when you push changed files!
<!-- But no worries, I'll explain every along the way! -->
No worries if that sounds a bit intimidating, I'll be here to guide you along the way!

## Setup now

<!-- First of all we will need to install the now command line tool. -->
<!-- First of all we will need to install now. -->
<!-- There are two versions  -->
<!-- You can either opt for the [full desktop version](https://zeit.co/download) or only install the [command line tools](https://zeit.co/docs/v2/getting-started/installation/). -->
<!-- Since installing the desktop app also installs the command line tool I'll leave the choice to you. -->
<!-- For completion sake I will include the  -->
To install now you'll have to install their desktop app.
No worries, it's minimalistic and keeps your `now` command line program automagically up-to-date!
You can either download it directly from [their website](https://zeit.co/download) or use `brew` to install it:

```sh
brew update
brew cask install now
```

I'll leave the choice to you.

After installation there should be a `now` command available on your command line.
You can test it by typing the following:

```sh
now --version
```

If you see some kind of version number and not an error than you're ready to go.
For me this prints `14.0.3`.

The only thing which is missing to finish the setup is to login into your now account.
If you don't have one yet then you can [create one here](https://zeit.co/signup).
After that is done simply type the following into your command line:

```sh
now login
```

This will prompt you for your email address, send you an email with a magic link which automagically logs you in.
Pretty neat, huh?

## Tell hugo to use relative URLs

Before we get to the fun part we need to make sure that certain configurations are properly set.
The config you copied earlier makes some choices which are not suitable for making quick deployments.

Run the following to check your config:

```sh
hugo config | grep -iE 'baseurl|canonifyurls'
```

If everything is fine this should just print:

```
canonifyurls = false
```

If it prints anything else (most notably a `baseurl` and/or `canonifyurls = true`) then please open your `config.toml`.
Now remove the `baseURL` and set `canonifyURLs` to `false`.

Why are we doing this you ask?
You see `canonifyURLs` tells hugo to create **absolute URLs** for everything.
That means your `baseURL` needs to point to the correct URL already.
But we want to do a quick deployment with an auto-generated URL from now, so obviously we don't know the `baseURL` until we deployed.

By removing the `baseURL` and setting `canonifyURLs` to `false` all the URLs will be **relative** which in turn will ensure that our page will be properly displayed.

With that out of the way, let's get to the fun part: building and deploying your page.

## Deploy right now!

Deployment with `now` is very, very simple:

```sh
# This builds your page
hugo

# This deploys your page
now --public public
```

*The `--public` flag tells now that we're okay with the files being publicly visible (at `/_src`).*

This will print something along the lines of:

```
Deploying ~/path/to/your/page/public under your-user-name
> Using project public
> Synced 1 file (37.95KB) [1s]
> https://public-abcdefghi.now.sh [v1] [in clipboard] [5s]
> Deployment complete!
```

And that's it!
Your page is deployed!

Now go visit the printed URL and if everything is fine it should look similar to this:

{{<
  image
    classes="fancybox"
    src="page-deployed1.png"
>}}

If it looks broken then please visit the [previous section on ensuring that hugo uses relative URLs]({{< ref "#tell-hugo-to-use-relative-urls" >}}).

## Now v1 or v2?

Shortly after I built this page now announced v2 of their service, which revolves around [builders](https://zeit.co/docs/v2/deployments/builders/overview/).
What we need is a **static deployment**; we run hugo once and use the resulting files as they are.
<!-- No backend logic necessary. -->
For that now offers a [static builder](https://zeit.co/docs/v2/deployments/official-builders/static-build-now-static-build/) which - when you take a look at the docs - actually uses hugo as an example.
Nevertheless I will talk on how to setup a v1 deployment using a Dockerfile, since that is what I use for this page!
But if you would rather use a v2 deployment, then go ahead!
No hard feelings.

<!-- Furthermore using a Dockerfile will also make migration  -->
<!-- Furthermore - if you ever decide to switch your hosting provider - a Dockerfile will give you more flexibility. -->





[hugo]: https://gohugo.io/
[now]: https://zeit.co/now
[github]: http://github.com/
[markdown]: https://daringfireball.net/projects/markdown/
[now]: https://zeit.co/now
