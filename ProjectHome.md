# Django layout templates using the Yahoo UI library #

This project provides a set of default [Django](http://www.djangoproject.com/) template layouts using the [Yahoo UI library](http://developer.yahoo.com/yui/) CSS tools ([Grids](http://developer.yahoo.com/yui/grids/), [Font](http://developer.yahoo.com/yui/fonts/), [Reset](http://developer.yahoo.com/yui/reset/), [Base](http://developer.yahoo.com/yui/base/)).  Just svn export to help you get you along your way with using the Django framework and/or [Google App Engine](http://code.google.com/appengine/).

Supported Yahoo UI versions:

  * 2.4.1
  * 2.5.2
  * 2.6.0

Also included are the following 8 layouts:

  * 1 column - full page width
  * 2 column - narrow left column (size of column can be changed)
  * 2 column - narrow right column (size of column can be changed)
  * 2 column - equal width columns
  * 3 column - equal width columns
  * 3 column - varying width columns (size of columns can be changed)
  * 3 column - 1/4 - 1/2 - 1/4
  * 4 column - equal width columns

There is also a base layout included in the layouts directory that contains all the defaults.

Feel free to add your comments or suggest a better (or another) layout!

  * [Installation](#Installation.md)
    * [Django](#Django.md)
    * [Google App Engine](#Google_App_Engine.md)
  * [Usage](#Usage.md)
    * [Overriding](#Overrides.md)
    * [Tips](#Tips.md)
    * [Links](#External_Links.md)

## Installation ##

**(If you're using anything < the latest Yahoo UI, check out the branches directory - this is where all the template layouts will be maintained.  I'll try to match trunk to the latest Yahoo UI library.)**

### Django ###

Export the layouts and install them in a directory where the Django templating system can find them.  (I typically install them in project\_name/templates/main\_site/layouts/).

The source code can be accessed by performing a Subversion export. For example, the following command will export the application's source code out to a templates directory:

```
svn export http://django-yui-layout-templates.googlecode.com/svn/trunk/ templates
```

Be sure to check the branches directory for any version < the latest Yahoo UI trunk

### Google App Engine ###

Export the layouts and install them in a directory named templates inside of your project directory.

The source code can be accessed by performing a Subversion export. For example, the following command will export the application's source code out to a templates directory:

```
svn export http://django-yui-layout-templates.googlecode.com/svn/branches/VERSION_HERE templates
```

The Google App Engine versions will only live in the branches directory.

## Usage ##

To use the layouts, you'll have to do 3 things.

  1. If you've exported the the files from svn, there should be a file called  '**layout\_overrides.html**'.  If not, create one in your main template directory.
  1. The base layout expects a file called '**header.html**' and '**footer.html**' in a directory called shared somewhere in your template path.  If you don't have this directory, either create one or keep reading to learn how to override the '**base\_layout.html**' settings. (Thanks akaihola!)
  1. Extend one of the provided Django template layouts in your template.
```
{% extends 'layouts/layout_2_equal_columns.html' %}
```

To add content to these layouts, there is a standardization on the block name you need to override in your templates.  The name of the block to add content to will be the column number (from left to right).  Using the example above, to add content to a layout, you'll have to put the following in one of your templates:

```
{% extends 'layouts/layout_2_equal_columns.html' %}

{% block 1 %}
Left Column
{% endblock 1 %}

{% block 2 %}
Right Column
{% endblock 2 %}

```

As you can see, block 1 is the left column, block 2 is the right column.  For a 3 column layout, block 1 would be the left column, block 2 would be the center column, and block 3 would be the right column. (Not too hard. :P).

### Overrides ###

To override any of the layout defaults, just place them in the **layout\_overrides.html** file.  To see what you can override, take a look at layout\_base.html.  As an example, you might want to override where the Yahoo UI css files are loaded from.  Currently, they're loaded from the Yahoo servers, but you might want to load it from your own CDN.  Taking a look at layout\_base.html, you'll see the following:

```
{% block css.shared %}
     <link rel="stylesheet" type="text/css" href="http://yui.yahooapis.com/2.6.0/build/reset-fonts-grids/reset-fonts-grids.css">
     <link rel="stylesheet" type="text/css" href="http://yui.yahooapis.com/2.6.0/build/base/base-min.css">
{% endblock css.shared %}
```

To override this default, just put the following in the layout\_overrides.html file.

```
{% block css.shared %}
     <link rel="stylesheet" type="text/css" href="http://path.to.your.cdn.network.com/css/files/reset-fonts-grids.css">
     <link rel="stylesheet" type="text/css" href="http://path.to.your.cdn.network.com/css/files/base-min.css">
{% endblock css.shared %}
```

Of course, this will override this default for **all** your layouts.  To override them in specific templates, just place the above code in your own template file.

### Tips ###

To remove spaces from your templates, inside one of your templates, you'll want to do something like the following:

```
{% block layout.base %}{% spaceless %}{{block.super}}{% endspaceless %}{% endblock layout.base %}
```

### External Links ###

To read more about how to configure the templates for Django, see the [Django Project documentation](http://www.djangoproject.com/documentation/templates/).  To read more about how to tweak these layouts, see the section on [template inheritance](http://www.djangoproject.com/documentation/templates/#template-inheritance). ({{block.super}} is your friend!).

**Voila! (Enjoy)**

If you have any suggestions, think there should be more layouts, or just want to talk story, feel free to contact us!