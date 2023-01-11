## Whats your take on the current Ruby on Rails Javascript Landscape and your preferred approach?

Rails provides a bunch of view helper methods written in Ruby to assist in generating HTML.
Sometimes, we want to add a little Ajax to those elements, and Rails has got us back in those cases.

- Because of Unobtrusive JavaScript, the Rails "Ajax helpers" are actually in two parts: the JavaScript half and the Ruby half.
- Unless we have disabled the Asset Pipeline, rails-ujs provides the JavaScript half, and the regular Ruby view helpers add appropriate tags to the DOM.
- Rails ships with the Turbolinks library, which uses Ajax to speed up page rendering in most applications.

When we are on Rails 7 it's totally different approach to working with Javascript:
When we create a Rails application, we will need to choose between import maps and a JavaScript bundling solution.

#### Import maps:

- Import maps the default in Rails 7
- Applications using import maps do not need Node.js or Yarn to function.
- If we plan to use Rails with importmap-rails to manage our JavaScript dependencies, there is no need to install Node.js or Yarn.

#### Traditional JavaScript bundler:

Other applications may still need a traditional JavaScript bundler. Requirements that indicate that we should choose a traditional bundler include:
- When our code requires a transpilation step, such as JSX or TypeScript.
- When we need to use JavaScript libraries that include CSS or otherwise rely on Webpack loaders.
- When we will install Bootstrap, Bulma, PostCSS, or Dart CSS through the cssbundling-rails gem.
- All options provided by this gem except Tailwind will automatically install esbuild for you if you do not specify a different option in rails new.

#### Hotwire (Turbo + Stimulus)

Hotwire, which is the combination of Stimulus and Turbo, became the default front-end framework for Rails applications.

We have detailed documentation for working with Hotwire on our GitHub handbook. 

Here are the references:
https://github.com/TecOrb-Developers/handbook/blob/main/rails/hotwire-turbo/info.md
https://github.com/TecOrb-Developers/handbook/blob/main/rails/hotwire-turbo/turbo_rules.md