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

This section will teach you two things:

1. how to use `now` to immediately put your page onto the web
2. how to build your page with `now`

Step 2 will then allow us to automate the whole process, so you just need to push your changes to github.
But no worries, I'll explain everything along the way!

# Is it hard?

# Alternatives?



[hugo]: https://gohugo.io/
[now]: https://zeit.co/now
[github]: http://github.com/
[markdown]: https://daringfireball.net/projects/markdown/
[now]: https://zeit.co/now
