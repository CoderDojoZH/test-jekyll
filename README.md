# Installing Jekyll for Github pages as a local project on Linux

Install Ruby as needed by Jekyll:

```sh
$ sudo apt-get install ruby-full build-essential zlib1g-dev
```

Get `gem` – the Ruby package manager – to install the packages into your home (no `sudo` needed) by adding to your `~/.bashrc` file:

```
# Install Ruby Gems to ~/gems
export GEM_HOME="$HOME/gems"
export PATH="$HOME/gems/bin:$PATH"
```

Read your new `.bashrc` file:

```
source ~/.bashrc
```

Install `bundler`, which will install gems locally to your project:

```sh
$ gem install bundler
```

In your project's directory, create a `Gemfile`

```sh
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

Install Jekyll in your project's directory:

```sh
$ bundle install --path vendor/bundle
```

## Creating the the scaffold

```sh
$ bundle exec jekyll new --force --skip-bundle .
```

Edit the `Gemfile` that has been created to get the same Jekyll version as installed on Github (instead of the current version):

- remove the line `$"jekyll", "3.3.0"`
- uncomment the line `gem "github-pages", group: :jekyll_plugins`
- run `bundle install`

## Running locally


```
$ bundle exec jekyll serve
```

## Updating the gems

```sh
$ bundle update
```

## English and german

- Create each page as a md file in each language and with different names.
- copy the theme (in the default install it's in the `minima` gem) `_include/header.html` and adjust the pages loop to:

```
{% assign pages=site.pages | where:"lang", page.lang %}
{% for my_page in pages %}
```

After the end the the `<header>` add the list of the languages:

```
<div class="wrapper" style="text-align: right; line-height: 2em">
  {% assign pages=site.pages | where:"ref", page.ref | sort: 'lang' %}
  {% for page in pages %} <a href="{{ page.url | prepend: site.baseurl }}" class="{{ page.lang }}">{{ page.lang }}</a> {% endfor %}
</div>
```
- warning: each page and language version must have a unique uri.
- add a `ref` and a `lang` field to the page's front matter.
- the `md` are named in english. the german pages get a `-de` suffix.
- `order` in the front matter defines the order in the navigation.

- without any plugin
  - https://www.sylvaindurand.org/making-jekyll-multilingual/
  - https://github.com/sylvaindurand/jekyll-multilingual
- the `Jekyll Multiple Languages Plugin` plugin
  - <https://www.klaasnotfound.com/2017/02/16/proper-multilingual-site-with-github-pages-and-jekyll/>
  - <https://github.com/Anthony-Gaudino/jekyll-multiple-languages-plugin>

## Pushing to Github (pages)

- If the page is for a repository, we need to set the name of the repository as the "baseurl" in the `_config.yml` file.

## Todo

- find out how to overload the scss with `_site/assets/main.scss` 

## Notes

Plugins: plugins do not work for gh-pages anyway

##  Resources

- https://jekyllrb.com/tutorials/using-jekyll-with-bundler/
- https://jekyllrb.com/docs/installation/ubuntu/
- https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/

