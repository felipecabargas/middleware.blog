---
author: juanpintoduran
title: '[Daily Tip] How to force existing column to contain data in Rails'
excerpt:
layout: post
categories:
  - Tips
tags:
  - rails
  - development
post_format: [ ]
---

First, create an empty migration, either by hand or using `bin/rails g`. Then use the `change_column_null` handle:

```ruby
class FieldNullOnModel < ActiveRecord::Migration[5.1]
	def change
		change_column_null :table_name, :column_name, false
	end
end
```

Save the changes and migrate (`bin/rails db:migrate`). Voila! The target column now requires content. Remember to update existing records to reflect this validation.
