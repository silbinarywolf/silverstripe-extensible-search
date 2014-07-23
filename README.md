# extensible-search

_**NOTE:** This is currently in development and may not function correctly._

	A module for SilverStripe which will allow user customisation and developer extension of a search page instance.

## Requirement

* SilverStripe 3.1.X

## Getting Started

* Place the module under your root project directory.
* Either define the full text YAML or retrieve a search wrapper module (such as Solr).
* `/dev/build`
* Configure your extensible search page.

## Overview

### Configuring the Search Page

A new page type `ExtensibleSearchPage` should automatically be created for you in the site root.
This should be published before you are able to perform searches using a search engine selection.

### Enabling Full Text

The extensible search page will work with the MySQL/SQLite full text search by default, however will require some YAML configuration around the data objects you wish to search against.

```yaml
FulltextSearchable:
  searchable_classes:
    - 'SiteTree'
SiteTree:
  create_table_options:
    MySQLDatabase:
      'ENGINE=MyISAM'
  extensions:
    - "FulltextSearchable('Title, MenuTitle, Content, MetaDescription')"
```

To allow search functionality through template hooks, make sure the appropriate extension has also been applied.

```yaml
Page_Controller:
  extensions:
    - 'ExtensibleSearchExtension'
```

The search form may now be retrieved from a template using `$SearchForm`.

### Custom Search Wrappers

These will need to be created as an extension applied to `ExtensibleSearchPage`, having their class name end with `SearchPage`.
