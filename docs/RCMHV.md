# RCMHV
Routes, controllers, models, helpers and views

## Routes
We use the default route rules for Rails to be consistent and not using **resources** since it makes the routes really unclear. Example routes:

```
GET 'photos', to: 'photos#index' # display a list of all photos
GET 'photos/new', to: 'photos#new' # return an HTML form for creating a new photo
POST 'photos', to: 'photos#create' # create a new photo
GET 'photos/:id', to: 'photos#show' # display a specific photo
GET 'photos/:id/edit', to: 'photos#edit' # return an HTML form for editing a photo
PUT 'photos/:id', to: 'photos#update' # update a specific photo
DELETE 'photos/:id', to: 'photos#destroy' # delete a specific photo
```

## Controllers
Make sure you keep the controllers as clean as possible as well as tiny as possible. Shift most code to helpers so we can reuse the methods.

If possible use models directly when you do not need to make any data mutations.

### Layouts
Override default layout with the layout option so every method in the controller will render the specified layout instead.

```plain
# Compare Controller
#
class CompareController < ApplicationController
  layout 'public'

...snip...
```

### Sessions
To make sure users have a valid session you can use the before\_action icw a method defined in your application\_controller, like:

```plain
# Tokens Controller
#
class TokensController < ApplicationController
  before_action :require_session

...snip...
```

The require\_session method could be something like:
```
# Application Controller
#
class ApplicationController < ActionController::Base
  def require_session
    return if session[:expiry] && session[:expiry] < Time.now

    redirect_to '/auth/login'
  end
```

## Models
Every model has it's db migration file. The database relations like primary keys or foreign keys are described in the migration and in the model.

Always add validations for references or indexes, the following is an example of a visitor model:

```
file: db/migrate/20240701000001_create_visitors.rb

class CreateVisitors < ActiveRecord::Migration[7.1]
  def change
    create_table :visitors do |t|
      t.string :first_name
      t.string :last_name
      t.string :email, null: false
      t.datetime :expected_arrival, null: false
      t.boolean :arrived, null: false, default: false
      t.references :user, foreign_key: true
      t.references :location, foreign_key: true

      t.timestamps
    end
    add_index :visitors, %i[email expected_arrival user_id location_id], unique: true
  end
end
```

The visitor model has a foreign key to user and location and it has a unique constraint on email with a scope.

```
file: app/models/visitor.rb

class Visitor < ApplicationRecord
  belongs_to :user
  belongs_to :location

  validates :email, uniqueness: { scope: %i[expected_arrival user location] }
end
```

Because we made the relations in the database but also in the model you can do the following:

```plain
irb(main):015> Visitor.first
#<Visitor:0x0000000120e18220
 id: 1,
 first_name: "Jeroen",
 last_name: "",
 email: "visitor@clearcodewizards.com",
 expected_arrival: Mon, 05 Aug 2024 06:00:00.000000000 UTC +00:00,
 arrived: true,
 user_id: 447,
 location_id: 5,
 created_at: Mon, 05 Aug 2024 09:14:20.907116000 UTC +00:00,
 updated_at: Mon, 05 Aug 2024 09:14:20.907116000 UTC +00:00>

irb(main):016> Visitor.first.user
#<User:0x0000000120c95510
 id: 447,
 email: "manager@clearcodewizards.com",
 first_name: "Manager",
 last_name: "Ofthings",
 address: nil,
 zipcode: nil,
 city: nil,
 phone: nil,
 active: true,
 created_at: Mon, 05 Aug 2024 09:14:13.333611000 UTC +00:00,
 updated_at: Mon, 05 Aug 2024 09:14:13.333611000 UTC +00:00>

irb(main):017> Visitor.first.location
#<Location:0x0000000120c56e00
 id: 5,
 name: "Office Clear Code Wizards",
 description: nil,
 address: "Testroad 19\n1234 AB TestCity",
 country: "Netherlands",
 phone: "012-34567890",
 created_at: Mon, 05 Aug 2024 09:14:10.518553000 UTC +00:00,
 updated_at: Mon, 05 Aug 2024 09:14:10.518553000 UTC +00:00>
```

## Helpers
When writing helpers make sure every method name is prefixed with the helpers name, this will help you make the code as readable as possible.

I.e. helper auth\_helper:

```
file: app/helpers/auth_helper.rb

module AuthHelper
  def auth_token
  end

  def auth_headers
  end

  def auth_get
  end
end
```

When you find auth\_.... methods in your code you directly know you need to look in app/helpers/auth\_helper.rb

## Views
Use as less conditions and data mutation as possible within the views, make sure the data is already in a state it should be when used in a view.

You can typically use helpers for this directly called from the view or indirectly via the global variables in controllers.

The use of partials are highly recommended in combination with hotwire:

[https://hotwired.dev/](https://hotwired.dev/)

