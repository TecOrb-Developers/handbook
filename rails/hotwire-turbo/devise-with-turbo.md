## Use Devise with Turbo

In Rails 7, hotwire's turbo intercepts with form actions and submits forms over the wire.

Currently, Devise gem does not support this action, hence needs a little tweaking to function well.

Here are couple of steps we need to configure to respond devise with TURBO_STREAM format

### Create a controller `turbo_devise_controller.rb`

Create a new controller and put below code inside. Here we are managing turbo_stream and html format response

````
class TurboDeviseController < ApplicationController
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
````

### Open config/devise.rb, we need to add configuration here

#### Add new class at the very top of this file

````
class TurboFailureApp < Devise::FailureApp
  def respond
    if request_format == :turbo_stream
      redirect
    else
      super
    end
  end

  def skip_format?
    %w(html turbo_stream */*).include? request_format.to_s
  end
end
````

#### Configure the parent class to the devise controllers.

`config.parent_controller = 'TurboDeviseController'`

#### Warden configuration

````
config.warden do |manager|
    #   manager.intercept_401 = false
    #   manager.default_strategies(scope: :user).unshift :some_external_strategy
    manager.failure_app = TurboFailureApp
end
````

#### Add Turbo stream configuration for navigation formats

`config.navigational_formats = ['*/*', :html, :turbo_stream]`


And we are done, restart your server check devise actions on your browser.
