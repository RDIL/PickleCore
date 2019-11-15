# PickleCore

*PickleCore* is a Jekyll theme developed by [Reece Dunham](https://github.com/RDIL) ([for his site](https://rdil.rocks)) and [Param Thakkar](https://github.com/paramt).

## Installation

First, download it by adding it to your `Gemfile`:

```ruby
gem "picklecore"
```

run bundler:

```shell
$ bundler
```

and then apply it in your `_config.yml`:

```yaml
theme: picklecore
```

and it should apply.

## Deploying

### GitHub Pages

Unfortunately, PickleCore is not whitelisted as a GitHub pages theme, so you can't use it by simply applying the theme. You will need to set up some kind of pipeline that bulids the site into raw HTML/CSS/JS and deploy that off the `gh-pages` branch.

### Netlify

Netlify is perfect for deploying PickleCore. The setup is quite easy - just set the command as `bundler exec jekyll build` and set the deploy folder to `_site`!

## Customization

PickleCore is (probably) the most customizable theme out in the Jekyllverse. Here is a list of keys you can put in your `_config.yml` and what they do:

* `name` - the name of the site (main title)
* `webmanifest` - link to a `manifest.json` or a file with the `.webmanifest` extension (used by Google for web apps, link must be relative to the root page of the site)
* `description` - description of the site (for metadata)
* `url` - the URL of your site when hosted in production
* `apple-touch-icon` - the URL of the Apple touch icon for the site if you have one (see [this article](https://www.computerhope.com/jargon/a/appletou.htm) for more info)
* `index_on_google` - `true` or `false` depending if you want your site in Google search results
* `keywords` - an inline list of comma (no spaces) seperated keywords (for SEO) (e.g. `keywords: "hello,world,this,is,my,site"`)
* `images` - stuff for favicons
    * Favicons - this requires multiple steps so read all sub-bullets
    * `images.favicon_base` - route of where the favicons are served, e.g. `https://my.site/favicons/favicon-` (extension must be `PNG`)
    * `images.favicons` - array of resolutions, e.g.:
    ```yaml
    images:
        favicons:
            - "32"  # 32x32
            - "64"  # 64x64
            # and so on
    ```
    * `images.tileimage` - the link to the Microsoft tile image
* `browserconfigxml` - link to a `browserconfig.xml` for Microsoft-based browsers
* The same thing can be applied to `twitter` with the subkey `image`, and `opengraph` with the subkey `image`
* `twitter` - Twitter meta dictionary
  * `username`: your Twitter username as a string (no `@`!)
* `devto` - your [DEV](https://dev.to/) username (if you want it on the sidebar)

Most of the favicons and images listed here can be made over at https://realfavicongenerator.net

### Colors

To change the base color, which defaults to `#303f9f`, you can add a file called `_includes/styling/theme-color.css`,
and put the hex color on the first line. **Do not** add a newline at the end of the file, it will break the CSS!

## Applying Theme Components

The PickleCore theme allows you to apply some nice looking components that match with the theme via `includes`.

### Cards

[![A card](https://raw.githubusercontent.com/RDIL/debugging-playground/master/card-example.png)](https://github.com/RDIL/PickleCore)

A card (shown above) can be applied by adding the following to any page **with [Front Matter](https://jekyllrb.com/docs/front-matter/) on it**:

```html
<!-- Note: you can put as many cards as you want in each card container, but all cards NEED to be in a container -->
<div class="cards">
  <!-- In this container, render a card -->
  {% include components/card.html cardtitle="My Card" cardbody="The text of the card!" %}
</div>
```

### Sidebar

The easiest way to apply the sidebar to your website is to use the `default-with-sidebar` layout via Jekyll:

```html
---
layout: default-with-sidebar
---
```

The second easiest way is to add it via the include:

```html
---
layout: default
---

<!--
    Anchor the sidebar opener to this location on the page
    Note: trying to move it via CSS may prove difficult!
-->

{%- include components/binds/sidebar-anchor.html -%}

<!-- Other content -->
```

But you should ***most certainly not*** simply use the `sidebar.html` component without the anchor - this will most likely break everything. Use one of the methods above.

> *Help! My sidebar is blank when I open it - what do I do?*
> Certain site config fields will populate the sidebar, so see the customization section above.
