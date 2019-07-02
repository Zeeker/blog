---
title: "How to build your professional website - Part 1: Build with Hugo"
date: 2019-03-18T01:00:00Z
categories:
- tech
- web
tags:
- website
- hugo
keywords:
- tech
- hugo
- markdown
- website
autoThumbnailImage: false
coverImage: /images/posts/how-to-build-your-professional-website/cover.jpg
coverCaption: Photo by Christopher Gower on Unsplash
coverSize: partial
# metaAlignment: center
showSummary: false
---

*This is part 1 of a 3 part series.*
*You can find the other parts here:*

1. *__[build your site using hugo][part-1]__*
2. *[deploy and host your page with now and setup your own domain][part-2]*
3. *[use github and now to automatically deploy everything on push][part-3]*

<!--toc-->

# Introducing [Hugo][hugo]

Hugo claims to be "the world’s fastest framework for building websites".
I have no idea if that's true but I can say that it's easy to setup, use, and produces great results.

<!-- But I'm getting ahead of myself. -->
<!-- In this section we will pretty much follow along [hugo's quickstart](https://gohugo.io/getting-started/quick-start/). -->
In this part we will mostly (but not exclusively) follow along [Hugo's quickstart](https://gohugo.io/getting-started/quick-start/).
So if you would rather read that, go ahead.
No hard feelings.
If you decide to do so, then you can skip this and go directly to [part 2 on how to deploy and host your page][part-2].

# Installing Hugo

Assuming you're on macOS installing Hugo is as simple as typing into your CLI (you'll need to have [brew](https://brew.sh/) installed):

```sh
brew install hugo
```

*[Click here to find out how to install Hugo for other platforms.](https://gohugo.io/getting-started/installing)*

<!-- After that you can create the basic framework of your future site by typing: -->
After that you can create your future site by typing:

```sh
hugo new site awesome-future-site
```

<!-- This will create a folder called (you might have guessed it) `awesome-future-site`. -->
This will create a folder named - you might have guessed it - `awesome-future-site`.
<!-- You could now use `hugo server` to see how it looks, but **spoiler** that would be pretty boring. -->
You could now use `hugo server` to see how it looks, but (**spoiler**) it's pretty boring.
By default Hugo generates an empty page with nothing in it.
So how do we make it pretty?

This is where themes come into play.

# Picking a theme

Hugo offers a number of themes, most of them contributed by the community.
In this tutorial I'll go with the [tranquilpeak theme][tranquilpeak] simply because it's the one you're looking at right now.
Feel free to look through [the other ones Hugo is offering](https://themes.gohugo.io/).

{{<
  figure
    caption="The Tranquilpeak Theme"
    src="tranquilpeak.png"
    link="https://themes.gohugo.io/hugo-tranquilpeak-theme/"
    target="_blank"
>}}

To install a theme you'll need to download it into the `themes` folder of your `awesome-future-site`.
How do you do that?
Going by Hugo's quickstart you should use `git` - this is also what I would suggest.

```sh
cd awesome-future-site

git init
git submodule add https://github.com/kakawait/hugo-tranquilpeak-theme.git themes/hugo-tranquilpeak-theme
```

In case the `git submodule` part doesn't make sense to you: it's basically a way of telling get to keep track of a "sub project".
Don't worry too much about it.
If you want to worry, you can read more about it [here](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

Okay, now we have the theme downloaded but how do we use it?
Great question, that's pretty easy!

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
Alternatively you can look at [my configuration on github](https://github.com/sascha-wolf/blog/blob/post/how-to-build-your-professional-website/config.yml).

# Content, content, content

Now that we have the foundations for your page it's time to start writing.

With Hugo this is done in [markdown][markdown].
<!-- If you're unfamiliar with markdown I would suggest to google for a tutorial, it's really simple and great to use. -->
If you're unfamiliar with markdown, I strongly suggest to take a look at it.
It's very, very simple so getting the basics will take you 5 minutes.
Check out [this awesome interactive tutorial](https://www.markdowntutorial.com/)!


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

The "block" on top will not be rendered in the final version.
Instead it serves as a place for your posts configuration.
Here you can specify things such as a cover and thumbnail image, the behaviour of the menu and so.
For details on the configuration I suggest to read the [relevant section in the tranquilpeak docs](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md#writing-posts).

<!-- You can now start typing away merrily and check your progress with `hugo server`.
To get an impression how a finished post might look like you can checkout [the markdown for this very post!](https://github.com/sascha-wolf/blog/blob/master/content/post/how-to-build-your-professional-website/index.md) -->
If you're curious on how a finished post might look like, why not checkout [the markdown for this very post?](https://raw.githubusercontent.com/sascha-wolf/blog/master/content/post/how-to-build-your-professional-website/part-1-hugo/index.md)
You might see some funny things in here, for example the `{{< raw "{{< figure ... >}}" >}}` stuff.
Hugo calls these [shortcodes](https://gohugo.io/content-management/shortcodes/) which act as simple snippets for things such as embedding YouTube videos etc.. Apart from this everything else should be pretty straightforward.

<!-- We could continue to talk about all the features of hugo but that would blow this post out of proportion. -->
There are other great things about hugo but that would blow this post out of proportion.
As it stands you should have all the tools at hand to generate your page.
<!-- There are more interesting things to come. -->
So what are you waiting for?

# And now?

<!-- Before we go on to the next section (hosting) let's quickly recap what we learned. -->
Let's recap!
<!-- We've learned how to create a basic page with hugo and how to write simple posts with it. -->
So far we've learned:

- how to install hugo
- how to use a theme, specifically the [tranquilpeak theme][tranquilpeak]
- how to create posts and that they are writen in [markdown][markdown]

All in all that's pretty good, so please give yourself a pat on the back.
Okay, done? Great!

<!-- But up until now everything was just locally. -->
<!-- But up until now everything happened on your computer. -->
The thing is: up until now everything only happened on your computer.
Nobody except you can see it.
<!-- The real question is: How do we get this on the web? -->
So, how do we get this on the web?

[Let's find out in the next part: Enter __now__!][part-2]

[hugo]: https://gohugo.io/
[tranquilpeak]: https://themes.gohugo.io/hugo-tranquilpeak-theme/
[markdown]: https://daringfireball.net/projects/markdown/

[part-1]: {{< ref "part-1-hugo" >}}
[part-2]: {{< ref "part-2-now" >}}
[part-3]: {{< ref "part-3-automation" >}}
