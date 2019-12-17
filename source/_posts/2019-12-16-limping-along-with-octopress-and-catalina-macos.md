---
layout: post
title: "Limping along with Octopress and Catalina macOS"
date: 2019-12-16 23:46
comments: true
categories: catalina macos octopress
---

I am still using the [Octopress 2 framework][octopress] for the website.  This has been challenging as the dependencies for old obsolete software gets harder and harder to satisfy.  However, it appears that I have succeed again for at least the Catalina release of macOS.

I found out I had a problem when I went to fix Disqus which had moved to `https://` protocol.  I found the files named disqus.html which had `http://` and changed it to `https://` but I was unable to regenerate the code due to a failure of the Octopress tool to run.

I use

```bash
chruby ruby-2.2.10
```

due to the yajl-ruby which won't build under later rubies.

My already built ruby-2.2.10 would not run because the openssl 1.0 version that had been linked in had disappeared (either due to Catalina or my migration to a new MacBook Pro.)  Rebuilding ruby with

```bash
ruby-install ruby-2.2.10
```

did not work nor did

```bash
ruby-install ruby-2.2.10 -- --with-openssl-dir=/usr/local/opt/openssl
```

did not work since the openssl was version 1.1.

After a fair bit of false steps, the successful approach was built around Chris Hobb's December 3, 2019 solution (for RVM) posted on [Stack Overflow](https://stackoverflow.com/questions/15511943/troubles-with-rvm-and-openssl).

First follow his steps (repeated here) to install openssl 1.0.2 by downloading openssl 1.0.2 from <https://www.openssl.org/source/>, and then building and installing it with

```bash
tar -xzf openssl-1.0.2t.tar.gz
cd openssl-1.0.2t
./Configure darwin64-x86_64-cc --prefix=/usr/local/opt/openssl@1.0
make
make test
sudo make install
```

and then adapting to `chruby` / `ruby-install` approach, build ruby 2.2.10 

```bash
ruby-install ruby-2.2.10 -- --with-openssl-dir=/usr/local/opt/openssl@1.0
```

Then going to the directory where I have the blog system and having previously deleted `Gemfile.lock`, I re-ran the install of gems into the `vendor` directory.

```bash
bundle install
```

Of course, in making this post, I issue

```bash
bundle exec rake new_post["Limping along with Octopress and Catalina macOS"]
```

Catalina has moved to using zsh instead of bash for its default shell.  Having taken the plunge, I found out that square brackets are used differently in zsh.  I was able to escape them to continue working:

```bash
bundle exec rake new_post\["Limping along with Octopress and Catalina macOS"\]
```
Thanks to [Qihuan Piao](http://kinopyo.com/en/blog/escape-square-bracket-by-default-in-zsh!) for this hint.

##One less groan 

Evidently the version of pigments used does not know about `zsh` so the code blocks have to be marked as `bash` instead of `zsh`.

Time to think about a supported framework.  Perhaps a migration to the modern version of Jekyll or a broader research into other static site tools that allow markdown content.

[octopress]: http://octopress.org