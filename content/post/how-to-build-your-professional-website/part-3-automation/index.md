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

<!-- Step 2 will then allow us to automate the whole process, so you just need to push your changes to github. -->
At the end of it you'll have a repository up on github and your page will be automagically deployed when you push changed files!
<!-- But no worries, I'll explain every along the way! -->
No worries if that sounds a bit intimidating, I'll be here to guide you along the way!

# Creating a github repo

Since the scope of this post is not "how to use GitHub", I'll keep this section short and sweet.
<!-- But if you've never created a repo before I'll link you to places which give lots input on how to do  -->

For this step you basically have two options:

1. use the official `hub` command line tool
2. navigate the web interface

If you wanna go with `hub` you can read about it [here](https://hub.github.com/).
<!-- It's a neat tool and I can highly recommend it. -->
It's basically GitHub on the command line and a neat tool.
I can highly recommend it.

On the other hand, if you prefer the web interface you can find everything in the [official docs from GitHub](https://help.github.com/en/articles/create-a-repo).
They're very thorough and should answer all your questions.

Now go, create a repository. 😉

# Setup now integration on github

Now that you have a GitHub repository it's time to create a link between it and your now account.
To achieve that we need to first link your GitHub account.

[Here](https://zeit.co/docs/v2/integrations/now-for-github/) is a link to the docs from now.
Nevertheless I'm gonna give you super quick bullet point rundown:

1. go to your [now account page](https://zeit.co/account)
2. look for a "GitHub Integration" section
3. press the "Install Now for GitHub" button
4. Login to GitHub, accept the prompt

That's it, easy right?
With the basic stuff out of the way we can get this part started! 🎉

# Now v1 or v2?

Shortly after I built this page now announced v2 of their service, which revolves around [builders](https://zeit.co/docs/v2/deployments/builders/overview/).
What we need is a **static deployment**: we run hugo once and use the resulting files as they are.
<!-- No backend logic necessary. -->
For that now offers a [static builder](https://zeit.co/docs/v2/deployments/official-builders/static-build-now-static-build/) which - when you take a look at the docs - actually uses hugo as an example.

<!-- Nevertheless I will talk on how to setup a v1 deployment using a Dockerfile, since that is what I use for this page! -->
Nevertheless in this guide I'll go with now v1 with a Dockerfile, it's what I use for deploying this page after all.
It's bit more involved - you'll have to write a Dockerfile - but I think it's a nice learning experience.

Nevertheless if you would rather use a v2 deployment, then go ahead!
No hard feelings.

# To Docker or not to Docker?

So, you might have heard of Docker but maybe you never used it.
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
<!-- [This guide][docker-guide] might be a good starting point. -->
If you're interested, [this official guide][docker-guide] is a really good starting point.

For now, all you need to know is this: we create Dockerfile which tells Docker how to build our *image*.
Let's jump right in and look at the Dockerfile which builds **this page**:

{{<
  github
    repo="zeeker/blog"
    file="Dockerfile"
>}}

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
If your build requires any secrets (which this one does not) it also protects you from leaking those secrets by accident.
<!-- (Technically you don't need to do this, it's just good practice to safe space.) -->
So while a multi-stage build is not strictly necessary, it is good practice.

That's it.
Feel free to use the Dockerfile from above and adjust it to your needs.

With that done we have completed the first step to full automation! 🎉

# now.json

How does now know which repositories are relevant?
For that you write a `now.json` file.

<!-- Instead of write lots of words about all the possible combinations you can configure  -->
I **could** bore you to death about all the things you can configure here.
But I won't.
Instead I'll show you the `now.json` for **this page**:

{{<
  github
    repo="zeeker/blog"
    file="now.json"
>}}

Ridiculously small, right?

Let’s go over each property:

- `alias`: you might have guessed it, this is the domain now should alias the deployed version to
- `name`: the name which appears in your now deployments and web interface, no magic here
- `type`: what kind of deployment is this? In this case it's `static` because now should just serve the files as they are
- `version`: what kind of now version do we wanna use?

So, how come now knows how to build my page?
This is a bit of magic on now's side:
<!-- when you have a `static` deployment and a `Dockerfile` now (correctly) assumes that this builds your page. -->
when you have a `static` deployment and a `Dockerfile` now (correctly) assumes that the image contains your final page.
The only thing you need to do is put the relevant files in a `/public` folder in your docker image.
[See here the docs] (https://zeit.co/docs/v1/static-deployments/builds/building-with-now/) for details on this.

All this in combination leads to now basically doing this:

1. fetch the files from the repo
2. detect the `Dockerfile`, run `docker build`
3. deploy the contents of the image's `/public` folder
4. alias the deployment to `blog.saschawolf.me`

Bonus: This also works locally!  
(It will skip the `alias` step though, so you can test things safely!)

To try it out you can just create your own version of the above `now.json` and simply run:

```sh
$ now
```

This will do steps 1-3 and give you a deployment you can peek at. 🙂
Neat, huh?

If you then like what you see you can just run:

```sh
$ now alias
```

And now will use the `alias` from your `now.json`.

# Push Sesame

And that's it!

You'll only need to push everything onto `master` in the repository created earlier.
**After that it will work automagically**.
Now will deploy any changes to `master` and alias it directly.
Other branches will get ignored, so you can safely use them for iterations on your posts.

What are you waiting for?
Create a page and push to `master`!

How do you think I published this blog post? 😉

*If you like this series you can follow me on Twitter [@wolf4earth](https://twitter.com/wolf4earth), on dev.to [@wolf4earth](https://dev.to/wolf4earth), or subscribe to the [RSS-Feed of this blog](https://blog.saschawolf.me/index.xml).*

[docker]: https://
[docker-guide]: https://docs.docker.com/get-started/
[hugo]: https://gohugo.io/
[now]: https://zeit.co/now
[github]: http://github.com/
[sw-blog]: https://blog.saschawolf.me/

[part-1]: {{< ref "part-1-hugo" >}}
[part-2]: {{< ref "part-2-now" >}}
[part-3]: {{< ref "part-3-automation" >}}
