---
layout: post
title: "Ruby on Rails: Perfecting Routing"
date: 2024-10-13 12:00:00 -0500
categories: [web development, ruby on rails]
tags: [routing, rails, restful, api]
---

In web development, simplicity and user ease are crucial. We aim to build apps that not only work well but also feel intuitive. Routing plays a big part here—Rails makes it an art.

## Rails Routing Magic

Rails is often called “magical,” and its routing proves this. The router does more than connect URLs to controllers—it generates routes and URLs, so you don’t have to hardcode strings in views.

### config/routes.rb: The Core of Routing

The routing magic happens in `config/routes.rb`. This file defines how requests should be handled, setting up which controllers respond.

## RESTful Routing with Resources

Rails lets you create RESTful routes with a single line. The `resources` method maps seven routes to controller actions, for example:

```ruby

Rails.application.routes.draw do
  resources :users
end

```

This simple declaration creates the following routes that align with REST principles.

1. GET /users (index)
2. GET /users/new (new)
3. POST /users (create)
4. GET /users/:id (show)
5. GET /users/:id/edit (edit)
6. PATCH/PUT /users/:id (update)
7. DELETE /users/:id (destroy)

## Singular Resources

If you need routes for a single resource, use `resource` instead:

```ruby

Rails.application.routes.draw do
  resource :profile
end

```
This skips the index route and uses singular names.

## Nested Routes

Nested routes show relationships between resources, aligning with ActiveRecord associations. For example:
if a `Figure` model has many `Comments`, you could represent this relationship in your routes:

```ruby

Rails.application.routes.draw do
  resources :figures do
    resources :comments
  end
end

```
This creates URLs like  `/figures/2/comments/4`, indicating that you're accessing the 4th comment of the 2nd figure.

### Best Practices for Nested Routes

1. **Be Specific**: Don't blindly nest resources. Hence only nest routes that make sense.

   ```ruby

   resources :figures do
     resources :comments, only: [:index, :new, :create]
   end

   ```

2. **Avoid Deep Nesting**: Stick to one level. Deeply nested routes can become hard to maintain.

3. **Use Shallow Nesting**: Use `shallow` for actions that don’t need the parent ID:

   ```ruby

   resources :figures do
     resources :comments, shallow: true
   end

   ```

## Advanced Routing Techniques

Once you’re comfortable with basics, explore advanced routes:

### Custom Routes

Sometimes, you need routes that don't fit the standard RESTful pattern. Rails allows you to define custom routes easily:

```ruby

get 'search', to: 'search#results'

```

### Constraints and Scopes

Match routes by constraints or group with scopes:

```ruby

get 'dashboard', to: 'users#dashboard', constraints: { subdomain: 'admin' }

```

Or use scopes to group routes with shared attributes:

```ruby

get 'dashboard', to: 'users#dashboard', constraints: { subdomain: 'admin' }
scope module: 'admin', path: '/admin' do
  resources :articles
end

```

### Namespace

Use namespaces for larger apps:

```ruby

namespace :api do
  namespace :v1 do
    resources :users
  end
end

```

This creates routes like `/api/v1/users` that map to controllers in `app/controllers/api/v1/`.

## Conclusion

Mastering Rails routing boosts both developer efficiency and user experience. Good routing follows REST principles, staying clear and simple. Remember, routes are the first connection to your app’s logic, so craft them well to set the stage for a robust app.

