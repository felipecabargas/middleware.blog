---
author: juanpintoduran
title: Tip of the day #2 - How to add extra fields during user registration with Devise
excerpt:
layout: post
categories:
  - Tips
tags:
  - rails
  - development
post_format: [ ]
---

Let's use the 'twitter clone' example from the rails tutorial. The Twitter registration is different, because it not only requires an `email` and `password` but also a `username`. Here is how you can add this extra field to your code:

First, let's import the default `devise` views into our project:

```bash
rails g devise:views
```

This will create a folder in `app/views/devise/` containing all the views required for (including the ones for `registration` that we will modify).

Create a new file and open it:

```bash
touch app/controllers/registrations_controller.rb
```

Inside the file, copy the following contents:

```ruby
class RegistrationsController < Devise::RegistrationsController

  private

  def sign_up_params
    params.require(:user).permit(:username, :email, :password, :password_confirmation)
  end

  def account_update_params
    params.require(:user).permit(:username, :email, :password, :password_confirmation, :current_password)
  end

end
```

Now, let's change the `config/routes.rb` file to use the new controller:

```ruby
devise_for :users, controllers: { registrations: 'registrations'}
```

Finally, open the 'New Sign Up' view (`app/views/devise/registrations/new.html.erb`) and add the extra field:

```erb
<div class="field">
  <%= f.label :username %><br />
  <%= f.text_field :username %>
</div>
```

Done! Restart your server and visit the sign up page (generally `/users/sign_up`).
