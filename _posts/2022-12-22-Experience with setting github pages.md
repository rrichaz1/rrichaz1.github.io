

Github has some great documentation and step by step instructions but like all documentation it can be incomplete. 
I have tried setting up blogs on my github pages website but always keep getting stuck.

The [landing page](https://docs.github.com/en/pages) starts with steps to create the repository. Then it sets off about [publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) and command line examples with jekyll. Running those commands do not work so I go back to searching foe how to set up Jekyll. 


The link [Use Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll) sent me another rabbits hole with click baits moving form one link to another. Now I just wanted to set up a baisc site to publish blogs. Wow!! relief [Base template for site ](https://github.com/skills/github-pages). I had high hopes that I will set up my blogs but I followed the steps still do not see links to the blogs.


Finally after some more searching found a [blog](https://www.aleksandrhovhannisyan.com/blog/getting-started-with-jekyll-and-github-pages/)


Ruby, bundler, jekyll installation on mac came with its hiccups, but now I was ready. The instruction said to `bundle exec jekyll new mysite` and waited with baited breath only to be disappointed. [Stack overflow](https://stackoverflow.com/questions/61704004/trouble-creating-a-new-jekyll-site-could-not-locate-gemfile-or-bundle-direct) to the rescue.
 

`
$ cd my-jekyll-website
$ bundle init
$ bundle add jekyll
$ bundle exec jekyll new --force --skip-bundle'

`bundle exec jekyll serve` and visit it at http://127.0.0.1:4000. Finally some kind of site still no lock with seeing the blog I laboriously created.


Now [changing the gem](https://github.com/github/pages-gem/issues/752) to github-pages did not work
`bundle add webrick

### Usefule links
[Markdown cheatsheet](https://www.markdownguide.org/cheat-sheet/)
[YAML cheatsheet](https://learntheweb.courses/topics/markdown-yaml-cheat-sheet/#yaml)
[Install jekyll on mac](https://jekyllrb.com/docs/installation/macos/)

https://abdullah85.github.io/pages-themes-previewer/github/pages/themes/2023/11/21/adding-additional-themes-with-dropdown.html

https://jekyll-themes.com/mmistakes/mm-github-pages-starter
https://jekyll-themes.com/sproogen/modern-resume-theme
https://github.com/jglovier/resume-template
