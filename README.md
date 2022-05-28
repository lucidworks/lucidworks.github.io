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
This site will parse the files in the site looking for markdown files.  The site structure users see is created virtually by the parser using the permalink information at the top of each readme file.  In the example above, using /AI/ in the permalink: field means that page will display at https://lucidworks.github.io/AI.  Further depth could be added with a value such as /AI/Lab1/. Note, the actual markdown file is in the eLearning folder in the GitHub repository.

