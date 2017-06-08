# Laravel Scout Algolia Macros

A collection of useful macros to extend Laravel Scout capability.

Laravel Scout added in version 3.0.5 the `Macroable` trait to the builder. It
means that you can know extend the builder according to your needs, without
having to extend a whole bunch of classes.

This package aims to provide a set of macros to take advantage of the
Algolia-specific feature.


## Installation

Pull the package using composer

```
composer install algolia/laravel-scout-algolia-macros
```

Next, you should add the `ScoutBuilderMacrosServiceProvider` to the `providers`
array of your `config/app.php` configuration file:

```php
Algolia\ScoutMacros\ScoutBuilderMacrosServiceProvider::class
```


## Usage

### `count`

The count method will return the number of results after the request to Algolia.

The point is to avoid pull data from the database and building the collection.

```php
$nbHits = Model::search('query')->count();
```

## `around`

The around method will add [geolocation parameter](1) to the search request. You
can define a point with its coordinate and the radius around it (in meters).

```php
//Models around Paris
Model::search('query')->around(48.8588536, 2.3125377, 10000)->get();
```

Where clauses can also be added

```php
Model::search('query')
    ->around(48.8588536, 2.3125377, 10000)
    ->where('something_id', 1)
    ->get();
```


## Contributing

Feel free to open an issue to request a macro.

Open any pull request you want, so we can talk about it and improve the package. :tada:

[1]: https://www.algolia.com/doc/guides/geo-search/geo-search-overview/
