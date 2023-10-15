---
layout: post
title: "Setting Up Pagy with Ajax-Datatables-Rails for Server-Side Pagination"
description: "Learn how to integrate Pagy for server-side pagination with Ajax-Datatables-Rails in your Ruby on Rails application."
category: Ruby on Rails
tags: [Ruby, Rails, Pagy, Datatables, Pagination]
---
{% include JB/setup %}

# Setting Up Pagy with Ajax-Datatables-Rails for Server-Side Pagination

Implementing server-side pagination can significantly improve performance, especially for applications with large datasets. In this blog post, you'll learn how to integrate Pagy with Ajax-Datatables-Rails to efficiently manage server-side pagination in a Ruby on Rails application.

## Why Use Pagy?

### Performance
Pagy is an extremely efficient pagination gem. It's up to 40 times faster than other pagination libraries, making it a perfect fit for high-performance applications.

### Simplicity
Pagy offers a straightforward syntax that integrates seamlessly with Ruby on Rails, reducing the complexity of your codebase.

## Setting Up Pagy

### Installation
First, add the Pagy gem to your `Gemfile`.

```ruby
gem 'pagy'
```

Then run the bundle install command to install the gem.

Create an initializer for Pagy in config/initializers/pagy.rb and customize the defaults to your liking - docs referenced at the end of this post.


## Integrating Ajax-Datatables-Rails

Installation
Add the following gem to your Gemfile:

```
gem 'ajax-datatables-rails'
```

Creating a Datatable Object
Create a new datatable object, for example, user_datatable.rb:

```
# app/datatables/user_datatable.rb
class UserDatatable < AjaxDatatablesRails::ActiveRecord
  extend AjaxDatatablesRails::Extensions::Kaminari
  # ... rest of your code
end
```
Implementing Server-Side Pagination
Modify your index action in the controller:

```
# app/controllers/users_controller.rb
def index
  respond_to do |format|
    format.html
    format.json { render json: UserDatatable.new(params, view_context: view_context) }
  end
end
```

```
# app/datatables/user_datatable.rb
class UserDatatable < AjaxDatatablesRails::ActiveRecord
  def get_raw_records
    @pagy, records = pagy(User.all)
    records
  end
end
```
## Conclusion

Integrating Pagy with Ajax-Datatables-Rails offers a robust, efficient solution for implementing server-side pagination. This combination not only enhances performance but also simplifies your codebase.