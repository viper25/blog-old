

# Site

[![Known Vulnerabilities](https://snyk.io/test/github/viper25/blog/badge.svg?targetFile=Gemfile.lock)](https://snyk.io/test/github/viper25/blog?targetFile=Gemfile.lock)

### Table of contents

- [Setup](#CustomSetup)
- [Drafts](https://jekyllrb.com/docs/posts//#drafts) 

## RSS
- Setup Your RSS with Feedburner - http://feedburner.google.com/
	http://feeds.feedburner.com/technikl
- Submit to Blog Directories - http://www.toprankblog.com/rss-blog-directories/
	http://technorati.com/
	
## SSL
https://hackernoon.com/set-up-ssl-on-github-pages-with-custom-domains-for-free-a576bdf51bc


## Pull Updates
https://github.com/techniklman/techniklman.github.io/compare/master...daattali:master

## Google Search Console
https://www.google.com/webmasters/tools/dashboard

## Google Custom Search
https://cse.google.com/cse/all

### TO DO:

Jekyll 4.0 comes with some major changes, notably:

  * Our `link` tag now comes with the `relative_url` filter incorporated into it.
    You should no longer prepend `{{ site.baseurl }}` to `{% link foo.md %}`
    For further details: https://github.com/jekyll/jekyll/pull/6727

  * Our `post_url` tag now comes with the `relative_url` filter incorporated into it.
    You shouldn't prepend `{{ site.baseurl }}` to `{% post_url 2019-03-27-hello %}`
    For further details: https://github.com/jekyll/jekyll/pull/7589

  * Support for deprecated configuration options has been removed. We will no longer
    output a warning and gracefully assign their values to the newer counterparts
    internally.
