# training-markdown.github.io
## This site is hosting the Lucidworks e-learning lab files.

### Setup
Setup has been compeleted on this site to allow hosting markdown and having it convert to HTML

The steps used to manually setup Jekyll for the markdown conversion can be found in the [GitHub Pages Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)

Now that the base Jekyll setup is complete and uploaded to the repo, pages can be added without further Jekyll setup.

### Adding a page
Pages can be added to the site adding the following lines to the top of a new markdown page

  ``---``  
  ``layout: page``  
  ``title: <your page title>``  
  ``permalink: <relative path, ex. /AI/>``  
  ``---``
  
### Site structure
All pages are physically in the root of this repo.  The site structure is created virtually by the parser using the permalink information.  In the example above, using /AI/ in the permalink: field means that page will display at https://SilverRat.github.io/AI.  Further depth could be added with a value such as /AI/Lab1/

### Theme Configuration
Additional themes can be applied via GitHub in the Settings / Page section. The default themes can have different elements (sections/styles) "overridden by placing the appropriate file replacements (or empty files) in the appropriate paths in the repo.  Basically, if the parser encounters a local file where the theme file would be in the repo, the local file takes over. Details on [GitHub Pages Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)  
