## Hotwire (Turbo + Stimulus)

With the release of Ruby on Rails 7 in December 2021, Hotwire, which is the combination of Stimulus and Turbo, became the default front-end framework for Rails applications.

- Stimulus has been out there for a while now, and it is a well-known library in the Rails ecosystem. 
- On the other hand, Turbo and its integration for Ruby on Rails are brand new tools with impressive features.
- Hotwire is a new approach to building web and mobile applications by sending HTML over the wire. 
- It includes Turbo, Stimulus.
- Hotwire is highly linked with Rails, it is completely language-agnostic, so it can work with other applications.

### Turbo
- Turbo and its integration for Ruby on Rails are brand new tools with impressive features.
- HTML drives Turbo at its core. 
- Turbo provides several techniques to handle HTML data coming over the wire and display it on your application without performing a full page reload. 
- Turbo is a continuation of the ideas from the previous [Turbolinks](https://github.com/turbolinks/turbolinks) framework
- Whereas Turbolinks previously just dealt with links, Turbo can now also process form submissions and responses. 
- This means the entire flow in the web application is wrapped into Turbo, making all the parts fast. 
- No more need for data-remote=true.

#### How Turbo works?
- Turbo automatically intercepts all clicks on `<a href>` links to the same domain.
- When you click an the link, Turbo prevents the browser from following it. Instead, Turbo changes the browser’s URL using the History API, requests the new page using fetch, and then renders the HTML response.
- During rendering, Turbo replaces the current `<body>` element outright and merges the contents of the `<head>` element. 
- The JavaScript window and document objects, and the HTML `<html>` element, persist from one rendering to the next.
- Turbo Drive can be disabled on a per-element basis by annotating the element or any of its ancestors with `data-turbo="false"`. 
- Turbo Drive automatically initiates a restoration visit when you navigate with the browser’s Back or Forward buttons.
- If you want Turbo Drive to be disabled by default, then you can adjust your import like this:
```
import { Turbo } from "@hotwired/turbo-rails"
Turbo.session.drive = false
```
- Use `data-turbo="true"` to enable Drive on a per-element basis.
- [Here is the complete documentation on turbo drive](https://turbo.hotwired.dev/handbook/drive)

Go through [turbo-rails documentation](https://github.com/hotwired/turbo-rails) for more technical details and uses with rails 