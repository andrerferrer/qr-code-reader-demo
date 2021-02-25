# GOAL

This is a demo to show-case how to implement .

[You can also check my other demos](https://github.com/andrerferrer/dedemos/blob/master/README.md#ded%C3%A9mos).

## What needs to be done?

### 1. Add the gem
```ruby
# Gemfile
gem 'rqrcode'
```
Remember to `bundle install`

### 2. Create a new feature to display the QR code
  * A new Route
  ```ruby
  # config/routes.rb
    resources :restaurants do
      member do
        get :qr_code
      end
    end
  ```
  * A new Controller#Action
  ```ruby
  # app/controllers/restaurants_controller.rb
  require 'rqrcode'
  class RestaurantsController < ApplicationController
    def qr_code
      @restaurant = Restaurant.find(params[:id])

      # this comes from the documentation
      qrcode = RQRCode::QRCode.new(restaurant_url(@restaurant))
      @svg = qrcode.as_svg(
        offset: 0,
        color: '000',
        shape_rendering: 'crispEdges',
        module_size: 6,
        standalone: true
      )
    end
  end
  ```
  * A new [View](app/views/restaurants/qr_code.html.erb)

Now, we can go to http://localhost:3000/restaurants/1/qr_code and see the QR code!
If you want to read this QR code with your smartphone, the app must be online (not on localhost).

---

And we're good to go 🤓
Good Luck and Have Fun
