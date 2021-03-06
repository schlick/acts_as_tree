# ActsAsTree [![Build Status](https://secure.travis-ci.org/amerine/acts_as_tree.png?branch=master)][travis]
[travis]: (http://travis-ci.org/amerine/acts_as_tree)


ActsAsTree extends ActiveRecord to add simple support for organizing items into parent–children relationships. By default, ActsAsTree expects a foreign key column called `parent_id`.

## Example

```ruby
class Category < ActiveRecord::Base
  acts_as_tree order: "name"
end

root      = Category.create("name" => "root")
child1    = root.children.create("name" => "child1")
subchild1 = child1.children.create("name" => "subchild1")

root.parent   # => nil
child1.parent # => root
root.children # => [child1]
root.children.first.children.first # => subchild1
```

We also have a convenient `Presentation` module you can mixin if you want a little visual representation of the tree strucuture. Example:

```ruby
class Category < ActiveRecord::Base
  extend ActsAsTree::Presentation

  acts_as_tree order: "name"
end

> Category.tree_view(:name)
root
 |_ child1
 |    |_ subchild1
 |    |_ subchild2
 |_ child2
      |_ subchild3
      |_ subchild4
=> nil
```

## Compatibility

We no longer support Ruby 1.8 or versions of Rails/ActiveRecord older than 3.0. If you're using a version of ActiveRecord older than 3.0 please use 0.1.1.

Moving forward we will do our best to support the latest versions of ActiveRecord and Ruby.

## Change Log
* 1.6.0 - April 21, 2014
	* Added new `leaves` method. See #23 -- MichalPokorny
* 1.5.1 - March 28, 2014
	* Fixing descendants modification bug. See #20 -- amerine, tmuerell
* 1.5.0 - December 16th, 2013
	* Added new `descendants` method -- adamkleingit
	* Fixed warning message -- akicho8
* 1.4.0 - June 25th, 2013
	* `Presentation#tree_view` -- rainchen
	* `root?` && `leaf?` methods. -- xuanxu
* 1.3.0 - March 29th, 2013
	* Rails 4.0 Support! -- mischa78
	* Readme Fixes -- mischa78 & seanhussey
* 1.2.0 - October 29th, 2012
	* Adding new `self_with_ancestors` accessor -- fbuenemann
	* `roots` is now a scope.
* 1.1.0 - April 24th, 2012
	* Deprecate the ActiveRecord::Acts::Tree module in favor of ActsAsTree
* 1.0.1 - April 18th, 2012
	* Include the Railtie for easier loading in Rails. Will reassess the forced module inclusion in the future.
* 1.0.0 - April 14th, 2012
	* Official 1.0 release. Force users to include the ActiveRecord::Acts::Tree module.
* 0.2.0 - April 9, 2012
	* Rails 3 Support
* 0.1.1 - February 3, 2010
	* Bug Fixes
* 0.1.0 - October 9th, 2009
	* First Gem Release

## Note on Patches/Pull Requests

1. Fork the project.
2. Make your feature addition or bug fix.
3. Add tests for it. This is important so we don't break it in a future version
   unintentionally.
4. Commit, do not mess with rakefile, version, or history. (if you want to have
   your own version, that is fine but bump version in a commit by itself so we can
   ignore when we pull)
5. Send us a pull request. Bonus points for topic branches.
6. All contributors to this project, after their first accepted patch, are given push
   access to the repository and are welcome as full contributors to ActsAsTree. All
   we ask is that all changes go through CI and a Pull Request before merging.

## License (MIT)

Copyright (c) 2007 David Heinemeier Hansson

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the 'Software'), to deal in the
Software without restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the
Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN
AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
