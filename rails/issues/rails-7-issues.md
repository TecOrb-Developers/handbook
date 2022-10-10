## Rails 7 Issues fixes

### link_to is not sending delete requests also confirm("Are you sure") not working.
Rails 7 use Hotwire & Turbo.js instead of webpacker (Was used in Rails 6).

We need to install turbo and stimulus manually:

    $ rails importmap:install 
    $ rails turbo:install stimulus:install

Also we will make sure to using `turbo_method` instead of `method` in `link_to` like:

    <%= link_to "Sign Out", destroy_user_session_path, data: { turbo_method: :delete }, class: "nav-link" %>

### render not working with Hotwire & Turbo.js?
As we know Rails 7 use Hotwire & Turbo.js. As per the rails documentaion we need to pass `status: :unprocessable_entity` while rendering.

````
render 'new', status: :unprocessable_entity
````

The above solution might work perfectly but in case we are using Devise above will add lots of effort because Devise uses render internally and we need to customize it every where. So another better solution is given below for devise.

### Issues - Rails 7 : How to use Devise with Hotwire & Turbo.js?

We need to create a turbo controller:
`````
class TurboController < ApplicationController
  class Responder < ActionController::Responder
    def to_turbo_stream
      controller.render(options.merge(formats: :html))
    rescue ActionView::MissingTemplate => error
      if get?
        raise error
      elsif has_errors? && default_action
        render rendering_options.merge(formats: :html, status: :unprocessable_entity)
      else
        redirect_to navigation_location
      end
    end
  end

  self.responder = Responder
  respond_to :html, :turbo_stream
end
`````

In *initializers/devise.rb* use this:
```
config.parent_controller = 'TurboController'
```