---
layout: post
title: "The 10 Most Underused ActiveRecord::Relation Methods"
date: 2012-04-14 22:51
comments: true
categories: ruby rails
---

Knee-deep in `ActiveRecord::Relation` code yesterday, I found some interesting nuggets that I had either had never heard of, or have seen far too rarely. Here I've gathered my top ten most underused relation methods from that list, for your reading delight.

<!-- more -->

### 10. `first_or_create` with a block

`first_or_create` is very familiar:

```ruby
Book.where(:title => 'Tale of Two Cities').first_or_create
```

and does exactly what it says. Often, though, you want to find a record with certain attributes, or create one with those _and_ additional attributes. To do this succinctly, you can supply a block to `first_or_create`:

```ruby
Book.where(:title => 'Tale of Two Cities').first_or_create do |book|
  book.author = 'Charles Dickens'
  book.published_year = 1859
end
```

### 9. `first_or_initialize`

If you don't want to save the record yet, you can use `first_or_initialize`:

```ruby
Book.where(:title => 'Tale of Two Cities').first_or_initialize
```

### 8. `scoped`

Sometimes you want an `ActiveRecord::Relation` representing all the records of a class. You can easily generate one using the `scoped` method:

```ruby
def search(query)
  if query.blank?
    scoped
  else
    q = "%#{query}%"
    where("title like ? or author like ?", q, q)
  end
end
```

### 7. `none`

Likewise, sometimes you want an `ActiveRecord::Relation` that contains no objects. Returning an empty array is usually not a great idea if the consumer of your API is expecting a relation object. Instead, you can use none.

```ruby
def filter(filter_name)
  case filter_name
  when :all
    scoped
  when :published
    where(:published => true)
  when :unpublished
    where(:published => false)
  else
    none
  end
end
```
### 5. `to_sql` and `explain`

`ActiveRecord` is great, but it doesn't always generating the queries you think it will. Jump in the console and run these commands on the relation you're building, to make sure it maps to a smart query, or that it's using the indices you lovingly crafted:

```ruby
Library.joins(:book).to_sql
# => SQL query for you database.
Libray.joins(:book).explain
# => Database explain for the query.
```

### 4. `find_by`

Rails code tends to be littered with lines like:

```ruby
Book.where(:title => 'Three Day Road', :author => 'Joseph Boyden').first
```

Instead, you can use the shortcut method `find_by`:

```ruby
Book.find_by(:title => 'Three Day Road', :author => 'Joseph Boyden')
```

which does exactly the same thing.

### 3. `scoping`

You can "scope" methods on a class to a particular relation. Consider the following example from the Rails documentation:

```ruby
Comment.where(:post_id => 1).scoping do
  Comment.first # SELECT * FROM comments WHERE post_id = 1
end
```

This is all kinds of useful.

### 2. `pluck`

Want an array of column values for certain records? I've seen this too many times:

```ruby
published_book_titles = Book.published.select(:title).map(&:title)
```

Or, even worse:

```ruby
published_book_titles = Book.published.map(&:title)
```

Instead, use pluck:

```ruby
published_book_titles = Book.published.pluck(:title)
```

### 1. `merge`

I couldn't live without this jewel, but it's strangely un-documented in the source, and not mentioned in any guide or book I've seen. Among other uses, it allows to do a join, and filter by a named scope on the joined model:

```ruby
class Account < ActiveRecord::Base
  ...
  def with_unread_messages
    joins(:messages).merge( Message.with_unread_messages )
  end
end
```