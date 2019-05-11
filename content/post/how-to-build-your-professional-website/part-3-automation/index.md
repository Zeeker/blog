---
draft: true
title: "How to build your professional website - Part 3: Automate it!"
date: 2019-04-19
categories:
- tech
- web
tags:
- website
- now
- github
- automation
- deployment
- docker
keywords:
- tech
- now
- zeit
- web
- website
- deployment
- docker
- automation
autoThumbnailImage: false
coverImage: /images/posts/how-to-build-your-professional-website/cover.jpg
coverCaption: Photo by Christopher Gower on Unsplash
coverSize: partial
# metaAlignment: center
showSummary: false
---

*This is part 3 of a 3 part series.*
*You can find the other parts here:*

1. *[create your site using hugo][part-1]*
2. *[deploy and host your page with now and setup your own domain][part-2]*
3. *[use github and now to automatically deploy everything on push][part-3]*

<!--toc-->

# Automate it!

For this section I'll assume you'll have the following setup:

- a now account ([create one here](https://zeit.co/signup))
- a github account ([create one here](https://github.com/join))

After this part you'll be able to push your code into a github repository and let now do all the deployment work for you.

<!-- ;;; REPHRASE -->
<!-- Step 2 will then allow us to automate the whole process, so you just need to push your changes to github. -->
At the end of it you'll have a repository up on github and your page will be automagically deployed when you push changed files!
<!-- But no worries, I'll explain every along the way! -->
No worries if that sounds a bit intimidating, I'll be here to guide you along the way!


# Now v1 or v2?

Shortly after I built this page now announced v2 of their service, which revolves around [builders](https://zeit.co/docs/v2/deployments/builders/overview/).
What we need is a **static deployment**; we run hugo once and use the resulting files as they are.
<!-- No backend logic necessary. -->
For that now offers a [static builder](https://zeit.co/docs/v2/deployments/official-builders/static-build-now-static-build/) which - when you take a look at the docs - actually uses hugo as an example.

<!-- Nevertheless I will talk on how to setup a v1 deployment using a Dockerfile, since that is what I use for this page! -->
In this guide I'll now v1 with a Dockerfile, it's what I use for deploying this page after all.
It's bit more involved - we need to create a Dockerfile after all - but I think it's a nice learning experience.

Nevertheless if you would rather use a v2 deployment, then go ahead!
No hard feelings.

# To Docker or not to Docker?

So, you might have heard of Docker but maybe you never used it.
<!-- !!! Verify -->
In a nutshell Docker is a generalized approach to package software with all it's dependencies.
To do this you write a Dockerfile.
A Dockerfile is basically a recepy which tells Docker how to package whatever you're trying to package.
<!-- The output of a Dockerfile (which is evaluated with `docker build`) is an *image*. -->
The output of a Dockerfile (evaluated with `docker build`) is an *image*.

<!-- I obviously can't go into the nitty gritty details on how Docker works here; if you're interested take a look at [this guide][docker-guide]. -->
<!-- I obviously can't go into the nitty gritty details on the terminology here or how Docker works. -->
While I obviously can't go into the nitty gritty details on the terminology here or how Docker works,
<!-- If you're interested take a look at [this guide][docker-guide]. -->
<!-- If you're interested there are lots of great guides out there explaining it way better than I ever could. -->
there are lots of great guides out there explaining it way better than I ever could.
<!-- !!! Add link to guide -->
<!-- [This guide][docker-guide] might be a good starting point. -->
If you're interested, [this official guide][docker-guide] is a really good starting point.

For now, all you need to know is this: we create Dockerfile which tells Docker how to build our *image*.
Let's jump right in and look at the Dockerfile which builds **this page**:

< link to github and Dockerfile here, shortcode? >

Doesn't look **too** scary (I hope).

In short, it installs hugo, downloads the theme, builds the page, and then does something ... odd.
<!-- The `FROM scratch` line tells Docker to, well, start the resulting image **from scratch** (with no software preinstalled). -->
The `FROM scratch` line tells Docker to, well, start the resulting image **from scratch**.
<!-- We then copy the built website from the previous image into this "from scratch" image. -->
Into this fresh image we copy the **built website** from the previous steps.
The end result is an image which **only contains the built site**.
No hugo installed, no theme downloaded, nothing.
In Docker-speech this is called a [multi-stage build](https://docs.docker.com/develop/develop-images/multistage-build/).

Why you may ask?
It makes the image very small since it only contains the files it needs to.
<!-- (Technically you don't need to do this, it's just good practice to safe space.) -->
While this is not strictly necessary, it is good practice to keep the image small and focused.


That's it.
Feel free to use the Dockerfile from above and adjust it to your needs.

With that done we have completed the first step to full automation! 🎉

# Creating a github repo

- Use the `hub` cli tool
- Via webinterface (link to docs)

# Setup now integration on github

Link to docs, some steps

# now.json

Configuration options, list relevant config here

# Push Sesame

And it works!

[docker]: https://
[docker-guide]: https://docs.docker.com/get-started/
[hugo]: https://gohugo.io/
[now]: https://zeit.co/now
[github]: http://github.com/
[sw-blog]: https://blog.saschawolf.me/

[part-1]: {{< ref "part-1-hugo" >}}
[part-2]: {{< ref "part-2-now" >}}
[part-3]: {{< ref "part-3-automation" >}}
