---
layout: post
title:  "Creating a Blogging Website with Jekyll"
categories: jekyll update
---
Jekyll is a powerful tool that can create a static website based on the content you write in some markdown or html text. It also provide useful utilities to create blogs. This blog, for one, is powered by Jekyll and I am going to talk about how you can make one too.

## Set-up and Create an Initial Site
### Installing Jekyll in your environment
Jekyll is based on Ruby programming language and it is a standard Ruby package called gem. So, first you have to make sure you have Ruby installed in your machine. You can check this by -

```
ruby -v
```

Make sure the version is `2.5.0` or higher. Also to install Jekyll which is a gem package you will need `gem` command line tool which should be shipped together with Ruby installation. You can check the version of `gem` by - 

```
gem -v
```

Then you can install Jekyll using `gem` command - 

```
gem install jekyll bundler
```

Notice that we are also installing `bundler` gem. Bundler gem manages dependencies for Ruby gems and reduce build error arises from version conflict.

### Creating your first site
First you want to create a directory where you want to put all your files and directories for your website in and optionally (but strongly recommended) mange them by version controlling tool like `git`. Say the directory name is `myBlog`. Create and to this directory from your terminal and run the following command -

```
jekyll new .
```

It will create the following directory strucutre -

```
myBlog
  |___ .gitignore
  |___ 404.html
  |___ about.markdoown
  |___ Gemfile
  |___ Gemfile.lock
  |___ index.markdown
  |___ _config.yml
  |___ _posts
          |___ <YYYY-MM-DD>-welcome-to-jekyll.markdown
```

Where YYYY-MM-DD will be the date that you ran this command. For example, I ran this today, so the file I got is `2023-04-09-welcome-to-jekyll.markdown`.

`.gitignore` : This file is mainly related to `git` tools. It tells git to ignore certain files from its version control. They should be mainly temporary files and can be generated any time by the build process so we do not need to keep track of them.

`404.html` : This page is shown when a user tries to go to a page/url in our site that does not exist.

`about.markdoown`, `index.markdown` : These are the markdown file which have the content to be displayed in the home page and the "About" page. When we will build the site Jekyll will convert them to an appropriate HTML format and put them in appropriate place. They need not be in markdown file, rather if you are comfortable with HTML you can write them in HTML format - just like the 404.html file.

`Gemfile`, `Gemfile.lock` : Gemfile contains all the gems that required to build our site and tells bundler to make sure to install the appropriate versions.

`_config.yml` : This is the configuration file for Jekyll. Here we can tell Jekyll about important information about how we want our site to be build. For example with the line `theme: minima` in the _config.yml file we are saying we want our site to be built based on a theme called minima.

`_posts` : Aside from pages, for a blogging site, we want to publish posts. Posts are same as pages but generally tied to a specific date. Jekyll make it easy to write post as we will see later.

### Test your site locally

Now that we have our initial content ready we can bulid our site by following command -

```
bundle exec jekyll serve
```

Jekyll will first build your site and put all the generated file for the site under `_site` directory. It will then create a server that will serve the site locally in `http://127.0.0.1:4000` address. Open up a browser and go to this address and you will be able to see the following page - 

![first webpage]({{ site.url }}/_assets/first_webpage.JPG)

Done! you got your first website!

## Adding a Page to the Site
You will notice that the there is a "About" page link in the top bar of our site. This is the page that is generated from the `about.markdown`. We might want to add more pages like this in our site, for example a "contact me" page. How do we do this. By defult Jekyll process any markdown or HTML files in the root directory when building the site. So it is easy to add a new page. For example just add a `contact_me.markdown` file with the following content - 

{% highlight markdown %}
---
layout: page
title: Contact Me
permalink: /contact_me/
---

If interested sent me an email at - `johndoe@exmaple.com`
{% endhighlight %}

Put the file in the root dir under `myBlog/` and reload the webapge (`http://127.0.0.1:4000`). You will see a new link for this new page in the top bar. Clicking the link will open up the following page - 

![contact me]({{ site.url }}/_assets/contact_me.JPG)

You might be wondering what is the content between the two `---`. These are called "Front Matter" and contain important metadata information that is used by Jekyll when building a page. Here -

`layout: page` : It tells Jekyll that this is a page and not a post. So Jekyll put the page link in the top bar.
`title: Contact Me` : This tells Jekyll to put "Contact Me" as the page title.
`permalink: /contact_me/` : This tells Jekyll how to format the url for this page. Look at the address above, it is - `http://127.0.0.1:4001/contact_me/`

When you have a of page like this you might want to create sub-directories to manage all the files. You can easily do this and Jekyll will still process them as before. For example create a directory `myBlog/topbar/` and put the `contact_me.markdown` under it and try building the site again. It will work same as before. 

But note that, Jekyll do not process files or directories that starts with the following characters -
- `_`
- `#`
- `.`
- `~`

If we do have this kind of files or directories we can still make Jekyll process them by including them in the `_config.yml` file using the `include` key. For example rename the `myBlog/topbar/` directory to `myBlog/_topbar/` and add the following line in the `_config.yml` -

```
include:
  - _topbar
```

Try building the site again - it will work the same way as before.


## Adding a Post to the Site
As mentioned previously blog is similar to pages but tied to a specific date. On the home page you will see a link of a post with title "Welcome to Jekyll" with date at top which is the day the post published. This page was created when we ran the `jekyll new` command.

If we want to create a new post we can just add a markdown or HTML under `_posts` directory. The name has to be of format `YYYY-MM-DD-<post-title>.markdown`. For example add a page named `2023-04-09-a-new-post.markdown` with the following content under `_posts` directory -

{% highlight markdown %}
---
layout: post
title: "A New Post"
categories: jekyll update
---

This is a new post!
{% endhighlight %}

Build the site again and you will see the new post under the previous one -

![new post]({{site.url}}/_assets/new_post.JPG)

## Some Jekyll Basics

Useful links -
- [Jekyll docs][jekyll-docs] - for complete guide on Jekyll.
- [Jekyll’s GitHub repo][jekyll-gh] - if you face any issue or want any features file them there 
- [Jekyll Talk][jekyll-talk] - ask any question you have 

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
