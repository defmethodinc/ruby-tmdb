# ruby-tmdb3

[![Build Status](https://travis-ci.org/defmethodinc/ruby-tmdb.svg)](https://travis-ci.org/defmethodinc/ruby-tmdb)

ruby-tmdb3 is an ActiveRecord-style API wrapper for [TheMovieDB.org (TMDb)](http://www.themoviedb.org/). ruby-tmdb3 uses tmdb's API v3 and is designed to streamline common tasks associated with finding information about movies and cast members.

## Installation

For ease of use ruby-tmdb3 is packaged as a Rubygem. Installing it is as simple as:

```console
gem install ruby-tmdb3
```

## Compatibility

Ruby 1.8.x & 1.9.x (2.0.x experimental)

## Examples

```console
require 'rubygems'
require 'ruby-tmdb3'

# setup your API key
Tmdb.api_key = "t478f8de5776c799de5a"

# setup your default language
Tmdb.default_language = "en"

@movie = TmdbMovie.find(:title => "Iron Man", :limit => 1)
# => <OpenStruct>

@movie.title
# => "Iron Man"
```

## Usage

There are 3 main methods you can use to get information about movies and cast members:

### TmdbMovie.find([:id, :imdb, :title, :limit, :expand_results, :language])

Find information about an individual movie, or a set of movies that share a similar title, eg:

```ruby
TmdbMovie.find(:title => "fight club", :limit => 10, :expand_results => true, :language => "en")
```

Parameters:

<dl>
<dt>:id<dt><dd>Specifies an individual movie via it's TMDb id</dd>
<dt>:title<dt><dd>Specifies a query string to look for in the movie titles</dd>
<dt>:imdb<dt><dd>Specifies an individual movie via it's IMDB id</dd>
<dt>:limit<dt><dd>Specifies the maximum number of results to be returned</dd>
<dt>:expand_results<dt><dd>The TMDb API by default returns only partial info for any API method that can return multiple results. When :expand_results is set to true ruby-tmdb3 automatically makes extra API calls to fetch the full information for each item. This can result in *very* slow requests though. If you only need basic information for a search listing then set this to false. Defaults to 'true'.</dd>
<dt>:language<dt><dd>Allows you to override the default API language on a per-query basis.</dd>
</dl>

You must supply at least one of :id, :title, or :imdb. All other parameters are optional.

### TmdbCast.find([:id, :name, :limit, :expand_results, :language])

Find information about an individual cast member, or a set of cast members sharing similar names, eg:

```ruby
TmdbCast.find( :id => 123, :name => "Brad", :limit => 1, :expand_results => true)
```

<dl>
<dt>:id<dt><dd>Specifies an individual cast member via their TMDb id</dd>
<dt>:name<dt><dd>Specifies a query string to look for in the cast names</dd>
<dt>:limit<dt><dd>See TmdbMovie</dd>
<dt>:expand_results<dt><dd>See TmdbMovie</dd>
<dt>language<dt><dd>See TmdbMovie</dd>
</dl>

You must supply at least one of :id or :name. All other parameters are optional.


## Usage Examples

Find all movies whose titles match a given string:

**@movies = TmdbMovie.find(:title => 'Iron Man')**

Find the movie most likely to be associated with a given title:

```ruby
@movie = TmdbMovie.find(:title => 'Sin City', :limit => 1)
```

Find a single movie by it's TMDb ID:

```ruby
@movie = TmdbMovie.find(:id => 187)
```

Find a single movie by it's IMDB ID:

```ruby
@movie = TmdbMovie.find(:imdb => 'tt0401792')
```

Find all cast members whose names match a given string:

```ruby
@actors = TmdbCast.find(:name => 'Fred')
```

Find an individual cast member via their TMDb ID:

```ruby
@actor = TmdbCast.find(:id => 101)
```

Get the info for a movie in French:

```ruby
@movie = TmdbMovie.find(:title => 'Sin City', :limit => 1, :language => "fr")
```

## Contributing

ruby-tmdb3 is maintained to work under Ruby 1.8.x & 1.9.x. Please make sure it works under both.

* Fork the repo.
* Create a topic branch.
* Push the topic branch to your fork.
* Create a pull request.


## Item information

To find out more about the information each object offers on retrieved items have a look at the [TMDb API Docs](http://help.themoviedb.org/kb/api/about-3). For the most accurate information about the information available have a look at the data directly through ruby-tmdb3 by calling @item.raw_data.inspect

## Author & Credits

The whole contributor list can be seen at [https://github.com/Irio/ruby-tmdb/graphs/contributors](https://github.com/Irio/ruby-tmdb/graphs/contributors).

Copyright (c) 2012 Irio Irineu Musskopf Junior.
Copyright (c) 2010 Aaron Gough, released under the MIT license.

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/Irio/ruby-tmdb/trend.png)](https://bitdeli.com/free "Bitdeli Badge")
