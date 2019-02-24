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

# Create your page using [hugo][hugo]

Hugo claims to be "the world’s fastest framework for building websites".
I have no idea if that's true but I can say that it's easy to setup, use, and produces great results.
<!-- But I'm getting ahead of myself. -->
In this section we will pretty much follow along [hugo's quickstart](https://gohugo.io/getting-started/quick-start/).
So if you would rather read that, go ahead.
No hard feelings.

So, assuming you're on macOS installing hugo is as simple as typing into your CLI:

```sh
brew install hugo
```

*[Click here to find out how to install hugo for other platforms.](https://gohugo.io/getting-started/installing)*

<!-- After that you can create the basic framework of your future site by typing: -->
After that you can create your future site by typing:

```sh
hugo new site my-great-future-site
```

<!-- This will create a folder called (you might have guessed it) `my-great-future-site`. -->
This will create a folder called - you might have guessed it - `my-great-future-site`.
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

# Is it hard?

# Alternatives?


[hugo]: https://gohugo.io/
[now]: https://zeit.co/now
[github]: http://github.com/
