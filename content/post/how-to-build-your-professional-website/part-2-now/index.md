---
title: "How to build your professional website - Part 2: Deploy with Now"
date: 2019-02-24T20:50:07+01:00
categories:
- tech
- web
tags:
- website
- now
- deployment
keywords:
- tech
- now
- zeit
- web
- website
- deployment
autoThumbnailImage: false
coverImage: cover.jpg
coverCaption: Photo by Christopher Gower on Unsplash
coverSize: partial
# metaAlignment: center
---

*This is part 2 of a 3 part series.*
*You can find the other parts here:*

1. *[create your site using hugo][part-1]*
2. *[deploy and host your page with now and setup your own domain][part-2]*
3. *[use github and now to automatically deploy everything on push][part-3]*

<!--toc-->

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

# Setup now

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

# Tell hugo to use relative URLs

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

# Deploy right now!

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

# A nice name for a nice page

<!-- Let's do a recap:

- we have created a (admittedly basic) page with hugo
- we have deployed this page with now -->
First give yourself a pat on the shoulder.
You have created a (admittedly simple) page and deployed it for everybody to see.

In theory you could go out and share this link with your friends, family, hairdresser, or whoever your heart desires.
But this link is not really **nice**, is it?

So, how can we get a nice link?
For example something like [blog.saschawolf.me][sw-blog]?

For that you need a **domain**.
There are basically two options right now:

1. you use a free subdomain from zeit
2. you buy a domain and use that

We'll look at both options but let's start with the first one.

## Now subdomains

Now allows you to **alias** your deployment.
Let's try it out:

```sh
# Alias your previous deployment to my-awesome-page.now.sh
now alias set public-abcdefghi.now.sh my-awesome-page.now.sh
```

*You probably need to swap out `my-awesome-page` with something else because I hog that subdomain. 😋*

If you're fine with this: great!
You can skip the rest of this section and read on.
If you want your truly own domain, then read on.

## Your own domain

[my-awesome-page.now.sh](https://my-awesome-page.now.sh) is pretty nice but it's not truly yours, you know?
So how can you get something like [blog.saschawolf.me][sw-blog]?

For that you'll have to **buy** a domain.
Lucky for us now allows you to buy domains directly from the command line.

For that to work you'll need to add a credit card to your account.
If that's an issue you'll probably need to use a difference service.
[Namecheap](https://www.namecheap.com/) for example accepts PayPal.
I can recommend them, I used them to buy this domain.

But let's assume you decided to buy your own domain from now and ensured it's available ([you can check that here](https://zeit.co/domains)).
All you need to do is run:

```sh
now domain buy my-great-domain.com
```

After you confirmed the purchase you can now alias your page:

```sh
now alias set public-abcdefghi.now.sh my-great-domain.com
```

And that's it.
No DNS fiddling.
No additional setup.
**It just works.**

Here a pro tip: You can also just run the latter command and now will **ask you** if you want to buy the domain.
Neat huh?

# What's next?

If you got until here: congratulations!

You're able to build your own page with hugo and deploy it to now.
But right now this involves a number of manual steps.

- you have to build your page
- you have to deploy it
- you have to alias it

Pretty tedious to do every time, right?
Let's automate it!

*[Continue with part 3: automate it!][part-3]*

[hugo]: https://gohugo.io/
[now]: https://zeit.co/now
[github]: http://github.com/
[markdown]: https://daringfireball.net/projects/markdown/
[now]: https://zeit.co/now
[sw-blog]: https://blog.saschawolf.me/

[part-1]: {{< ref "part-1-hugo" >}}
[part-2]: {{< ref "part-2-now" >}}
[part-3]: {{< ref "part-3-automation" >}}
