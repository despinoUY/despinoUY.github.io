---
layout:  post
title:   "Some interesting things about Jekyll's Minima theme"
image_alt: {
    url: "https://upload.wikimedia.org/wikipedia/commons/4/42/Jekyll_%28software%29_Logo.png",
    source: "Wikimedia"
}
image:   "https://upload.wikimedia.org/wikipedia/commons/4/42/Jekyll_%28software%29_Logo.png"
excerpt: "If you are having some problems customizing Minima theme, this post is worth reading."
date:    2019-06-27 00:00:00 -0300
categories: [Jekyll, Minima, Blogging, Development, English]
---

As you can see (and it's also stated at the footer), this site's theme is based on Minima. You may think that using this theme and following its documentation to customize it to your taste might be easy. Awfully, it's not. So, in order to help whoever it needs it, I'm writing this post. Let's start!

## SASS root file in Minima

At the [official documentation](https://github.com/jekyll/minima/) of this theme, you'll find that you must import Minima SCSS at `<your-site>/assets/css/style.scss`. Well, that's not particularly correct...

In fact, the CSS generated by this theme finally locates at `<your-site>/_site/assets` and it's called `main.css`. So, the SASS file should be located at `<your-site>/assets` and should be called `main.scss` in order to work.

## What about pagination?

Well, when you are displaying the homepage and you want to paginate the results, this is more straight forward. First of all you need to include the `jekyll-pagination` plugin in your Gemfile and in your `_config.yml` under `plugins` as stated [here](https://jekyllrb.com/docs/pagination/) (this applies if you are using Jekyll 3 or higher). As you are including a new gem in the project, you must also bundle the whole project in order to download this new gem.

After this, you might want to customize this, so first open the `_config.yml` again. After the `plugins` section you can set up how many posts you want to display per page (you set the `paginate` variable) and the path each page will have (this under the `paginate-path` variable). The path should vary per each page, so to make this possible using the page number is helpful. Using `:num` will give us the page number where the items can be found, starting at 2.

If you choose to use a immediate URL (by saying this I mean using a URL that doesn't use subdirectories - i.e. `/page-:num`), when bundling and serving this project, you might find that the console shows a warning message:

{% highlight console %}
Pagination: Pagination is enabled, but I couldn't find an index.html page to use
as the pagination template. Skipping pagination.
{% endhighlight %}

This happens because Jekyll uses by default an `index.md` file for its index. `jekyll-pagination` gem looks for an HTML file, so it fails on loading. So you must change its extension to HTML by renaming it to `index.html`. If you use subdirectories (let's say you want to head pages to `blog/page-:num`), you must generate a new `index.html` file under a `blog` directory in the root dir of this Jekyll project with the same content of the file I mentioned previously.

