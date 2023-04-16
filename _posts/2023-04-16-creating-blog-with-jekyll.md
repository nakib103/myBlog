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
First you want to create a directory where you want to put all your files and directories for your website in and optionally (but strongly recommended) mange them by version controlling tool like `git`. Say the directory name is `myBlog`. Create the directory and from there run the following command -

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

Where YYYY-MM-DD will be the date that you ran this command. For example, I ran this today, so the file I got is `2023-04-16-welcome-to-jekyll.markdown`.

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

![first webpage]({{ site.url }}/assets/first_webpage.JPG)

Done! you got your first website!

You might be wondering why my url says `http://127.0.0.1:4001` instead of `http://127.0.0.1:4000`. Because, I had already a site serving at `http://127.0.0.1:4000` address (which is actually this blog) and I cannot run another site in same address. So with some useful jekyll command I setup this test webiste in different port -

```
bundle exec jekyll serve --port 4001
```


## Adding a Page to the Site
You will notice that the there is a "About" page link in the top bar of the site. This is the page that is generated from the `about.markdown`. We might want to add more pages like this, for example a "contact me" page. How do we do this. By defult Jekyll process any markdown or HTML files in the root directory when building the site. So it is easy to add a new page. For example just add a `contact_me.markdown` file with the following content - 

{% highlight markdown %}
---
layout: page
title: Contact Me
permalink: /contact_me/
---

If interested sent me an email at - `johndoe@exmaple.com`
{% endhighlight %}

Put the file in the root dir under `myBlog/` and reload the webapge (`http://127.0.0.1:4000`). You will see a new link for this new page in the top bar. Clicking the link will open up the following page - 

![contact me]({{ site.url }}/assets/contact_me.JPG)

You might be wondering what is the content between the two `---`. These are called "Front Matter" and contain important metadata information that is used by Jekyll when building a page. Here -

`layout: page` : It tells Jekyll that this is a page and not a post. So Jekyll put the page link in the top bar.

`title: Contact Me` : This tells Jekyll to put "Contact Me" as the page title.

`permalink: /contact_me/` : This tells Jekyll how to format the url for this page. Look at the address above, it is - `http://127.0.0.1:4001/contact_me/`

When you have a lot of pages like this you might want to create sub-directories to manage all the files. You can easily do this and Jekyll will still process them as before. For example create a directory `myBlog/topbar/` and put the `contact_me.markdown` under it and try building the site again. It will work same as before. 

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

![new post]({{site.url}}/assets/new_post.JPG)

## Some Jekyll Basics


### Front Matter
Front matter is a YAML snippet and should be place at the top of a page (or post) between two tripple dashed line, for example, in the above section in the post we use the following front matter - 

{% highlight markdown %}
---
layout: post
title: "A New Post"
categories: jekyll update
---
{% endhighlight %}

Front matter are generally used to define variable and use them in page (or post) using Liquid objects. There are some pre-defined variable that mean something special, for example `title: "A new Post"` will set the title of the page.

### Liquid
Liquid is a templating language for Jekyll. If you have worked with Django, it is similar to the template language that Django offers. There are 3 main components for Liquid -

#### Objects
They are predefined variables that you can access by using double curly braces, for example - {%raw%}`{{ page.title }}`{%endraw%}. Use it anywhere in your markdown or HTML, Jekyll will put the page title instead. You can add variable in the front matter and access them through `page.<variable name>`. For example we defined a variable `var: example` in the front matter and this value here - `{{ page.var }}` printed using liquid {%raw%}`{{ page.var }}`{%endraw%}.

#### Tags
Tags are represented by a pair of curly braces and percentage sign inside - {%raw%}`{%`{%endraw%} and {%raw%}`%}`{%endraw%}. They define the logic and control flow for templates. For example we can use `if` statement using tags -

```
{%raw%}{% if page.var %}{%endraw%}
  We have variable called named var.
{%raw%}{% endif %}{%endraw%}
```

#### Filters
With filters we can change the output of a Liquid object. They are used in a object separted by `|`. For example we can capitialize our {%raw%}`{{ page.var }}`{%endraw%} variable by using {%raw%}`{{ page.var | capitalize }}`{%endraw%} which will interpret `{{ page.var }}` as `{{ page.var | capitalize }}`.

### Layouts
Layouts are used to remove duplicacy of code. For example if you are to have a same navigation bar in each of your pages it is not a good practice to write it in every page markdown or HTML. Layout are template HTML which can be used by other pages and posts. For example, look at follwing template file `default.html` - 

{% highlight HTML %}
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{%raw%}{{ page.title }}{%endraw%}</title>
  </head>
  <body>
    <p>This page uses default template!</p>
    {%raw%}{{ content }}{%endraw%}
  </body>
</html>
{% endhighlight %}

Here the {%raw%}`{{ content }}`{%endraw%} is a special Liquid object that returns the rendered content of the page the layout is used upon. Let us use this template in a page. First put the template `deafult.html` file in the `_layouts` directory. Then update the `contact_me.markdown` - 

{% highlight markdown %}
---
layout: default
title: Contact Me
---

If interested sent me an email at - `johndoe@exmaple.com`
{% endhighlight %}

You will see the line `This page uses default template!` appearing at the top of your "Contact me" page.

### Includes
Include is similar to layout as it let you use another file into your page. The difference is that you build your page content onto your layout (your page content gets rendered in {%raw%}`{{ content }}`{%endraw%} tag in the layout), on the other hand, include add the content from another file into your page. It uses the {%raw%}`{% include %}`{%endraw%} tag to do the magic. 

Write the following content in a `header_line.markdown` file and put the file in `_includes` directory. 
{% highlight markdown %}
This is my awesome blogpost!
{% endhighlight %}

Now you can use this file in any markdown or HTML, for example your `contact_me.markdown` - 

{% highlight markdown %}
---
layout: page
title: Contact Me
permalink: /contact_me/
---

{%raw%}{{ include header_line.markdown }}{%endraw%}

If interested sent me an email at - `johndoe@exmaple.com`
{% endhighlight %}


Good luck creating your first blog website using Jekyll!


Some Useful links -
- [Jekyll docs][jekyll-docs] - for complete guide on Jekyll.
- [Jekyll’s GitHub repo][jekyll-gh] - if you face any issue or want any features file them there 
- [Jekyll Talk][jekyll-talk] - ask any question you have 

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
