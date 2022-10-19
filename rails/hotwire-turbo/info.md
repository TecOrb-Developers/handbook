## Hotwire (Turbo + Stimulus)

With the release of Ruby on Rails 7 in December 2021, Hotwire, which is the combination of Stimulus and Turbo, became the default front-end framework for Rails applications.

- Stimulus has been out there for a while now, and it is a well-known library in the Rails ecosystem. 
- On the other hand, Turbo and its integration for Ruby on Rails are brand new tools with impressive features.
- Hotwire is a new approach to building web and mobile applications by sending HTML over the wire. 
- It includes Turbo, Stimulus.
- Hotwire is highly linked with Rails, it is completely language-agnostic, so it can work with other applications.

### Turbo

Turbo speeds up Rails applications, reduces the amount of JavaScript we have to write, and makes it easy to work with real-time features. The best part of it is that it's simple to learn

- Turbo and its integration for Ruby on Rails are brand new tools with impressive features.
- Turbo provides several techniques to handle HTML data coming over the wire and display it on your application without performing a full page reload. 
- Turbo is a continuation of the ideas from the previous [Turbolinks](https://github.com/turbolinks/turbolinks) framework
- Whereas Turbolinks previously just dealt with links, Turbo can now also process form submissions and responses. 
- This means the entire flow in the web application is wrapped into Turbo, making all the parts fast. 
	- No more need for data-remote=true.
	- Easy to lazy-load independent parts of the page.

#### Turbo Drive: (Form responses must redirect to another location)
 
Turbo Drive is the first part of Turbo, which gets installed by default in Rails 7 applications, as we can see in our Gemfile and our JavaScript manifest file application.js.

After using Turbo drive, all clicks on links and form submissions are now AJAX requests

- which speeds up our applications. 
- We get this benefit for free as it does not require any work; 
- we only have to import the library.

Suppose we have created a simple CURD rails application and we have added presense true on an attribute in model.  This CRUD application is already a single-page application by default due to Turbo Drive, and we had no custom code to write.

Now we are testing on browser, The app works as expected unless **(Here is an issue)**:
- We submit an empty form and the validation failed (we will render back to new/edit form create/update actions). 
- Even if we have a presence validation on the attribute of the model, the error message is not displayed as we could expect when the form submission fails. 
- If we open the console in our dev tools, we will see the cryptic error message "Form responses must redirect to another location".

This is a "breaking change" since Rails 7 because of Turbo Drive. 

If you ever encounter this issue, the way to fix it is to add `status: :unprocessable_entity` to YoursController#create and YoursController#update actions when the form is submitted with errors:

```
	if @entity.save
      redirect_to entity_path, notice: "Entity successfully created."
    else
      # Add `status: :unprocessable_entity` here
      render :new, status: :unprocessable_entity
    end
```

After response status code added, our CRUD is now working perfectly.

