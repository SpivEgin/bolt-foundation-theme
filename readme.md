Foundation for Bolt Theme
=========================

Foundation for Bolt is a blank theme for Bolt, built on top of
[Zurb Foundation for sites 6](http://foundation.zurb.com/). To learn more about
specific Foundation components, check out the
[Foundation 6 Documentation](http://foundation.zurb.com/sites/docs/).

The documentation laid in this README will cover how to get started with
Foundation for Bolt and how some Foundation components, are integrated with
Bolt.

Features included with Foundation for Bolt?
-------------------------------------------

Foundation for Bolt comes with all of the great features that are found in the
Zurb Foundation framework, and a few things more. Simply put, if it works in
Foundation, it will work in Foundation for Bolt. The theme also includes:

 - Sass(scss) or CSS Versions
 - Multiple Foundation Navigation and layout options
 - Optional Bower and Gulp Support
 - And much, much more!

Requirements for Foundation for Bolt
------------------------------------

You can use whatever you want – seriously. You can use CodeKit, Grunt, Compass
or nothing at all. It’s completely up to you how you decide to build your theme
– Foundation for Bolt will stay out of your workflow as much as possible.

This theme does include Bower and Gulp files, and is optimized for a Gulp-based
workflow. To get the most out of Foundation for Bolt, Gulp is highly
recommended. However, if you're not using Gulp yet, you can also modify the
compiled CSS files as is.

File Structure
--------------

These are the most important files, included in this theme.

```
.
├── css/
│   ├── foundation.css       - The compiled Foundation CSS framework
│   └── theme.css            - Theme-specific CSS
├── images/                  - Image files for this theme are put here
├── js/
│   ├── app.js               - Theme-specific Javascript
│   ├── foundation.js        - The compiled Foundation javascript library
│   └── jquery.min.js        - The jQuery javascript library
├── partials/
│   ├── _aside.twig          - Partial for the sidebar. With fixed content, or widgets
│   ├── _footer.twig         - Partial for the footer below every page
│   ├── _fresh_install.twig  - Partial that's shown on fresh installs with some instructions
│   ├── _header.twig         - Partial for the header banner with the site title.
│   ├── _master.twig         - Twig template, that is uses to 'extend' all pages (See 'template inheritance')
│   ├── _recordfooter.twig   - Partial with meta-information below a page or entry
│   ├── _sub_menu.twig       - Partial with macro for rendering the drop-down menu
│   └── _topbar.twig         - Partial containing the top menu bar
├── source/
│   ├── scss/
│   │   ├── _settings.scss   - SCSS source file for Foundation. Is used by `css/foundation.css`
│   │   ├── foundation.scss  - SCSS source file for Foundation. Is compiled to `scss/foundation.scss`
│   │   └── theme.scss       - SCSS source file for the theme. Is compiled to `css/theme.css`
│   ├── .babelrc             - Helper file for gulp / npm
│   ├── bower.json           - Configuration for used Bower packages.
│   ├── gulpfile.js          - Build task script for Gulp.
│   └── package.json         - Configuration for used Node / Gulp packages.
├── CHANGELOG.md             - List of versions, and their respective changes.
├── index.twig               - Template used for 'home'
├── listing.twig             - Template used for 'listings', like `/pages` or `/category/movies`
├── notfound.twig            - Template used for the '404 not found' pages
├── page.twig                - Template used for single record pages, like `/page/lorem-ipsum`
├── readme.md                - This file. :-)
├── record.twig              - Generic template used for single record pages, that don't have a specific template set.
├── search.twig              - Template used for listing search results.
├── styleguide.twig          - Static page, that shows all Foundation elements on one long page. Go to `/styleguide` to see it in the browser.
└── theme.yml                - Theme-specific configuration.
```

Installation
------------

To install this theme, simply search for 'Foundation' in Bolt's backend, and
click the buttons.

Alternatively, download the `.zip` or `.tgz` file from the [bobdenotter/bolt-
foundation-theme Github repository](https://github.com/bobdenotter/bolt-
foundation-theme/releases). Extract the file, and place the `foundation` folder
in your `theme` folder. Don't forget to set `theme: foundation` in your
`config.yml` file.

Getting Started
---------------

This theme was developed to be as "tinker friendly" as possible. Depending on
your area of expertise and experience with different front-end development
techniques, you can modify the CSS of this theme on different 'levels':

 - If you're familiar with Foundation and gulp, you can finetune which parts of
   Foundation are included, as well as all their settings. See the
   `source/scss/foundation.scss` and `source/gulpfile.js` files.
 - If you do know a bit of SCSS, you can work in `source/scss/theme.scss` and
   `source/scss/_settings.scss` files.
 - Otherwise you can just make your changes in the compiled css at `css/theme.css`.

The templates themselves are the `.twig` files in the root of the theme folder,
as well as the additional helper files in the `partials` folder.

Modifying the HTML of the theme
-------------------------------

All HTML parts of the theme are made in Twig. If you're not familiar with Twig
yet, be sure to read the Bolt documentation on Twig, as well as the official
Twig documentation.

This theme uses a concept called 'template inheritance'. From other themes or
CMS'es, you might be familiar with seeing each page 'include' a header and a
'footer'. Instead, we have one 'master' template, which are extended by each of
the different templates. You can read more about this concept on the
[Twig site - Template Inheritance](http://twig.sensiolabs.org/doc/tags/extends.html)
or here: [Dealing With Themes And Layouts With Twig](http://hugogiraudel.com/2013/11/12/themes-layouts-twig/)

For example, take a look at one of the simpler templates, `record.twig`:

```twig
{% extends 'partials/_master.twig' %}

{% block main %}

        <h1>{{ record.title }}</h1>

        {{ fields() }}

        {% include 'partials/_recordfooter.twig' with { 'record': record } %}

{% endblock main %}
```

You'll notice the first line that states that the template 'extends' the
`_master.twig` partial. The rest of the template is the `{% block %}`, which
overrides the 'main' block in the master template. Inside the block is just an
`<h1>`-tag with the record's title, a `{{ fields() }}` tag that will output the
fields that are defined for this contenttype, and it closes with an include of
`_recordfooter.twig` to display some meta data, like the author, date and
permalink.

As you can see, we can still use 'include' for small blocks of HTML, even though
we're using template inheritance. This way we can keep our themes very
structured and organized.

In the diagram below, you'll see the wat most pages are structured. In this case,
`index.twig`. In the HTML, you will see it extends `_master.twig`, which can be found in
the `partials/` folder. Inside this file, the global structure of all pages is laid out:
The basic HTML structure, and a handful of other included partials.

```
 index.twig structure                     _topbar.twig

                                               │
                     ├─────────────────────────┴────────────────────────────────┤

                    ┌────────────────────────────────────────────┬───────────────┐
 _sub_menu.twig ──▶ │  Home link1 link2 link3                    │______ [Search]│ ◀── _search.twig
                    ├────────────────────────────────────────────┴───────────────┤
                    │••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••│
                    │•••••••••••••••••••••••(header image)•••••••••••••••••••••••│ ◀── _header.twig
                    │•••••••••••••••••••••••(name of site)•••••••••••••••••••••••│
                    │••••••••••••••••••••••••••••••••••••••••••••••••••••••••••••│
                    │ ┌──────────────────(main content)─┐ ┌────────────(aside)─┐ │
                    │ │Lorem ipsum dolor sit amet       │ │Lorem ipsum dolor   │ │
                    │ │                                 │ │sit amet. Consec-   │ │
                    │ │Consectetur adipiscing elit. Nunc│ │tetur adipiscing.   │ │
                    │ │omni virtuti vitium contrario    │ │                    │ │
                    │ │nominehgpponitur. Non enim, si   │ │Latest X            │ │
                    │ │malum est dolor, carere eo malo  │ │ - intellegetur     │ │
                    │ │satis est ad bene vivendum. Duo  │ │ - Expectoque       │ │
                    │ │Reges: constructio interrete.    │ │ - videantur        │ │ ◀── _aside.twig
                    │ │                                 │ │                    │ │
                    │ └─────────────────────────────────┘ │Latest Y            │ │
                    │ ┌─────────────────────────────────┐ │ - intellegetur     │ │
                    │ │Lorem ipsum dolor sit amet       │ │ - Expectoque       │ │
                    │ │                                 │ │ - videantur        │ │
                    │ │Consectetur adipiscing elit. Nunc│ │                    │ │
                    │ │omni virtuti vitium contrario    │ │                    │ │
                 ┬  ├─┴─────────────────────────────────┴─┴────────────────────┴─┤
  _footer.twig ──┤  │ (C) 2016                          Home link1 link2 link3   │ ◀── _sub_menu.twig
                 ┴  └────────────────────────────────────────────────────────────┘

                   ├────────────────────────────┬─────────────────────────────────┤
                                                │

                                           _master.twig
```


Working with the `.scss` files
------------------------------

This theme uses NPM, Gulp and bower to run the tasks to compile and minify the
Sass files.

If you don't have Node and Gulp running yet, install it from
[Nodejs.org](https://nodejs.org) and run the following command from the command
line:

```
npm install -g bower gulp
```

If you're new to Gulp, these two tutorials on the subject might be of interest
to you:

 - https://markgoodyear.com/2014/01/getting-started-with-gulp/
 - https://travismaynard.com/writing/getting-started-with-gulp

Note that we're using ES6, so you _might_ find yourself in "NPM dependency
hell". If you do, your best bet would be to make sure you've updated your Gulp,
Bower and NPM to their respective latest versions. To do so, just run `npm
install -g bower gulp` again. You might also need to update Node and NPM:

```
sudo npm cache clean -f;
sudo npm install -g n;
sudo n stable
```

Next, to install the local Bower and NPM modules, run:

```
npm install
bower install
```

Now you can simply run `gulp` to compile the javascript and sass files. When
developing, you'll want to run:

```
cd foundation/source
gulp
```

This will run gulp, and it will continue to monitor changes to the `.scss`
files. If you make a change, the compiled files will be updated immediately.
When you're ready to deploy, and put the site in production, be sure to build
the files and minify them:

```
gulp build --production
```

This will build the files that you can deploy, or put into your versioning
system.


