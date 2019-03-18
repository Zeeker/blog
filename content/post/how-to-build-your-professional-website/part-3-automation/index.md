---
draft: true
title: "How to build your professional website - Part 3: Automate it!"
date: 2019-02-24T20:50:07+01:00
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
[sw-blog]: https://blog.saschawolf.me/

[part-1]: {{< ref "part-1-hugo" >}}
[part-2]: {{< ref "part-2-now" >}}
[part-3]: {{< ref "part-3-automation" >}}
