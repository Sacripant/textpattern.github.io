---
layout: document
category: Tags
published: true
title: Article custom
description: The article_custom tag provides a variety of custom options for sorting, selecting, and displaying articles.
tags:
  - Article tags
---

# Article custom

On this page:

* [Syntax](#syntax)
* [Attributes](#attributes)
* [Examples](#examples)
* [Genealogy](#genealogy)

## Syntax

~~~ html
<txp:article_custom />
~~~

The **article_custom** tag is a *single* or a *container* tag that provides a variety of custom options for sorting, selecting, and displaying articles (the tag will be replaced with one or more articles).

If used as a container, it must be specified as an opening and closing pair of tags, like this:

~~~ html
<txp:article_custom>
    ...contained statements...
</txp:article_custom>
~~~

This is equivalent to putting the contained statements into a form named 'my_form' and using `<txp:article_custom form="my_form" />`.

Unlike the [article](article) tag, `<txp:article_custom>` will always return an article list and **is not context-sensitive**. This means while the [article](article) tag can only see posts within the currently viewed section/category/author and so forth, `<txp:article_custom />` can see all posts from all sections, categories and authors unless you restrict it via attributes (see below), thus context-sensitive navigation tags, such as [older](older) and [newer](newer), will not work.

`<txp:article_custom />` offers many additional attributes that `<txp:article />` does not.. but only `<txp:article />` will produce the full single article page. If you have only `<txp:article_custom />` on a page, rather than `<txp:article />`, then you will never reach the permalinked article page - you'll always get an article list page.

However, you can have the added features and functionality of `<txp:article_custom />`, while keeping the necessary `<txp:article />` in full force by using conditionals: `<txp:if_individual_article>` and `<txp:if_article_list>`, e.g.:

~~~ html
<txp:if_article_list>
    <txp:article_custom form="myform" limit="10" category="ideas" section="article" sort="Posted desc" />
</txp:if_article_list>

<txp:if_individual_article>
    <txp:article />
</txp:if_individual_article>
~~~

## Attributes

Tag will accept the following attributes (**case-sensitive**):

`allowoverride="boolean"`
: Whether to use override forms for the generated article list.
: **Values:** `0` (no) or `1` (yes).
: **Default:** `0`.

`author="author name"`
: Restrict to articles by specified author(s) **login name**.
: **Values:** (comma separated list of) author login name(s).
: **Default:** unset, retrieves from all authors.

`category="category name"`
: Restrict to articles from specified category/categories. Note: the category names may be different to the title you typed when you created the category, as the names are sanitized for URL use. Check the [Categories administration panel](https://docs.textpattern.io/administration/categories-panel) to ensure you are using the correct names.
: **Values:** (comma separated list of) category name(s).
: **Default:** unset, retrieves from all categories.

`customfieldname="value"`
: Restrict to articles with specified value for specified custom field name. Replace *customfieldname* with the actual name of the custom field.
: Important: Using dashes `-` or spaces may cause errors or render this feature ineffectual. Underscores in both custom field names and values are confirmed to work.
: **Default:** unset.

`excerpted="boolean"`
: Restrict to articles with/without an excerpt.
: **Values:** `0` (no, return all) or `1` (yes, return only those containing an excerpt).
: **Default:** `0`.

`exclude="article id(s)"` <span class="footnote warning">v4.6.0+</span>
: Exclude a specific article or list of articles (each ID separated by a comma).
: **Default:** unset.

`expired="boolean"` <span class="footnote warning">v4.5.0+</span>
: Whether to include articles that have expired or not.
: **Values:** `0` (no, don't include expired articles) or `1` (yes, include expired articles).
: **Default:** Setting of preference 'Publish expired articles'.

`form="form name"`
: Use specified form template to process each article.
: **Default:** `default`.

`frontpage="boolean"`
: Include only those articles with 'Section appears on front page?' set on the [Sections administration panel](https://docs.textpattern.io/administration/sections-panel). If set to `1`, only such articles are displayed, otherwise they are all displayed.
: **Values:** `0` (no) or `1` (yes).
: **Default:** `0`.

`id="article ID"`
: Display the specific article or list of articles (each ID separated by a comma).
: Important: When a list is supplied, this does **not** imply a sort order (see **Example 6** below).
: **Default:** unset.

`keywords="keyword(s)"`
: Restrict to articles with specified keyword(s).
: **Default:** unset.

`limit="integer"`
: The number of articles to display.
: **Default:** `10`.

`month="yyyy"/"yyyy-mm"/"yyyy-mm-dd"`
: Restrict to articles posted within the specified year/month/day.
: **Default:** unset.

`offset="integer"`
: The number of articles to skip.
: **Default:** `0`.

`section="section name"`
: Restrict to articles from specified section(s).
: **Values:** (comma separated list of) section name(s).
: **Default:** unset, retrieves from all sections.

`sort="sort value(s)"` <span class="footnote warning">v4.0.4+</span>
: How to sort the resulting article list. Specify a value from the ones below, followed by a space and then add either `asc` or `desc` to sort in ascending or descending order, respectively. **Note:** values are case sensitive on some servers.
: **Values:** \\
`AuthorID` (author name). \\
`Category1`. \\
`Category2`. \\
`comments_count`. \\
`custom_n` where `n` is the number of your custom field - for numeric values use `(custom_n+0)`. \\
`Expires` (expiry date). \\
`ID` (article id#). \\
`Image` (article image id#). \\
`Keywords`. \\
`LastMod` (date last modified). \\
`LastModID` (author name of last modification). \\
`Posted` (date posted). \\
`rand()` ([random](https://dev.mysql.com/doc/refman/5.7/en/mathematical-functions.html#function_rand)). \\
`Section`. \\
`Status`. \\
`Title`. \\
`url_title`. \\
Each field in the `textpattern` database table can be used as a sort key.
: **Default:** `Posted desc`.

`status="status"`
: Restrict to articles with the specified `status`.
: **Values:** `live` or `sticky`.
: **Default:** `live`.

`time="time"`
: Restrict to articles posted within specified timeframe.
: **Values:** `past`, `future` or `any` (both `past` and `future`).
: **Default:** `past`.

### Common presentational attributes

These attributes, which affect presentation, are shared by many tags. Note that default values can vary among tags.

`break="value"` <span class="footnote warning">v4.0.7+</span>
: Where value is an HTML element, specified without brackets (e.g. `break="li"`) or some string to separate list items.
: **Default:** `br` (but see [break cross-reference](https://docs.textpattern.io/tags/tag-attributes-cross-reference#break) for exceptions).

`class="class name"`
: HTML `class` to apply to the `wraptag` attribute value.
: **Default:** tag name or unset (see [class cross-reference](https://docs.textpattern.io/tags/tag-attributes-cross-reference#class)).

`label="text"`
: Label prepended to item.
: **Default:** unset (but see [label cross-reference](https://docs.textpattern.io/tags/tag-attributes-cross-reference#label) for exceptions).

`labeltag="element"`
: HTML element to wrap (markup) label, specified without brackets (e.g. `labeltag="h3"`).
: **Default:** unset.

`wraptag="element"` <span class="footnote warning">v4.0.7+</span>
: HTML element to wrap (markup) list block, specified without brackets (e.g. `wraptag="ul"`).
: **Default:** unset (but see [wraptag cross-reference](https://docs.textpattern.io/tags/tag-attributes-cross-reference#wraptag) for exceptions).

## Examples

### Example 1: Display 5 articles from a specific section on the homepage

To show 5 articles from a 'news' section within the homepage `default` page template (or the template you use for displaying your homepage), add:

~~~ html
<txp:article_custom section="news" limit="5" form="homepage_articles" />
~~~

Then create an 'article' type form template called `homepage_articles`, containing:

~~~ html
<article>
    <h1>
        <txp:title />
    </h1>
    <txp:if_article_image>
        <p>
            <txp:article_image />
        </p>
    </txp:if_article_image>
    <txp:body />
</article>
~~~

Other tags used: [article_image](article_image), [body](body), [if_article_image](if_article_image), [title](title).

### Example 2: List articles published in specified month

~~~ html
<txp:article_custom form="month_list" sort="Section asc" month="2004-14" />
~~~

This code will display a monthly list articles by section and in ascending order, between the years of 2004 and 2014. See **Example 5** below for more information on article sorting.

### Example 3: Select by keyword

~~~ html
<txp:article_custom sort="Posted desc" keywords="One" />
~~~

This code will display articles that have a keyword with a value `One`.

### Example 4a: Select by author (using single tag)

~~~ html
<txp:article_custom form="author_list" author="Parkling" />
~~~

This code will display articles that have a authored by author with login name of `Parkling`. The referenced `author_list` article form might go thus:

~~~ html
<p>
    <txp:permlink>
        <txp:title />
    </txp:permlink>
</p>
~~~

Other tags used: [permlink](permlink), [title](title).

### Example 4b: Select by author (using container tag)

~~~ html
<txp:article_custom author="Parkling">
    <p>
        <txp:permlink>
            <txp:title />
        </txp:permlink>
    </p>
</txp:article_custom>
~~~

This is exactly equivalent to **Example 3a**, just using a container tag instead of a single tag with referenced form.

Other tags used: [permlink](permlink), [title](title).

### Example 5: Combined with custom fields

~~~ html
<txp:article_custom colour="red" />
~~~

This code will display articles that have a custom field named `colour` with a value `red`.

### Example 6: Article sorting

~~~ html
<txp:article_custom sort="AuthorID asc, Posted asc" />
~~~

Uses the `sort` attribute to define values by which to order article output. In this case two values are declared. `AuthorID asc` first orders articles alphabetically by author names, then `Posted desc` orders them by date published (`desc` meaning newest to oldest).

Why might you do it? Sorting is a powerful way to group articles (e.g. by author), and/or give priority to articles most recently published (typically better for your website visitors).

### Example 7: Select by article ID(s)

~~~ html
<txp:article_custom id="81,73" />
~~~

Outputs articles specified by list of IDs, in this example that would be articles `81` and `73`. Order of articles may not match the order of the IDs in the list, that depends on what `sort` ordering you have specified, for example:

~~~ html
<txp:article_custom id="81,73" sort="field(id,81,73)" />
~~~

Outputs articles specified by list of IDs, in the order given in the `sort` field.

## Genealogy

### Version 4.6.0

`exclude` attribute added.

### Version 4.5.0

`expired` attribute added.

### Version 4.0.7

Can be used as a container tag. \\
`id` attribute can take a comma-separated list of IDs. \\
`wraptag` and `break` attributes added.

### Version 4.0.6

Support added for comma separated lists for `section`, `category` and `author` attributes.

### Version 4.0.4

`listform` attribute deprecated (it never made a difference to `article_custom` anyway). \\
`sort` attribute added (replaces `sortby` and `sortdir` attributes). \\
`sortby` and `sortdir` attributes deprecated.
