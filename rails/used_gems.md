## [Tecorb developers rails](https://github.com/TecOrb-Developers/handbook/blob/main/rails) / Used Popular Gems
Here are some of the popular gems which we have used in our codebase.

### Authentication and Authorization Gems
- devise: https://github.com/heartcombo/devise
- devise password-less auth:https://github.com/abevoelker/devise-passwordless
- devise-two-factor: https://github.com/tinfoil/devise-two-factor
- omniauth: https://github.com/omniauth/omniauth
- doorkeeper: https://github.com/doorkeeper-gem/doorkeeper
- action_policy: https://github.com/palkan/action_policy
- rolify: https://github.com/RolifyCommunity/rolify
- jwt_sessions: https://github.com/tuwukee/jwt_sessions

### Gems to manage various level of security layers
- brakeman: https://github.com/presidentbeef/brakeman
- rack-attack: https://github.com/rack/rack-attack
- bundler-audit: https://github.com/rubysec/bundler-audit
- secure_headers: https://github.com/github/secure_headers
- doorkeeper: https://github.com/doorkeeper-gem/doorkeeper
- bundler: https://github.com/rubygems/bundler

### Gems to manage Role-based permissions & control
- cancancan: https://github.com/CanCanCommunity/cancancan
- pundit: https://github.com/varvet/pundit

### Gems used in Testing (TDD/BDD)
- rspec-rails: https://github.com/rspec/rspec-rails
- factory_bot: https://github.com/thoughtbot/factory_bot
- parallel_tests: https://github.com/grosser/parallel_tests
- mechanize: https://github.com/sparklemotion/mechanize
- database_cleaner: https://github.com/DatabaseCleaner/database_cleaner
- database_cleaner-active_record: https://github.com/DatabaseCleaner/database_cleaner-active_record
- database_cleaner-redis: https://github.com/DatabaseCleaner/database_cleaner-redis
- faker: https://github.com/faker-ruby/faker
- shoulda-matchers: https://github.com/thoughtbot/shoulda-matchers
- simplecov: https://github.com/simplecov-ruby/simplecov

### Gems to implement Scheduled and Recurring Jobs
- sidekiq: https://github.com/mperham/sidekiq
- sidekiq-cron: https://github.com/ondrejbartas/sidekiq-cron
- sidekiq-failures: https://github.com/mhfs/sidekiq-failures
- sidekiq-status: https://github.com/utgarda/sidekiq-status

### Gems to implement Search
- elasticsearch-ruby: https://github.com/elastic/elasticsearch-ruby
- ransack: https://github.com/activerecord-hackery/ransack
- pg_search: https://github.com/Casecommons/pg_search

### Gems to implement distributed locks
- redlock-rb: https://github.com/antirez/redlock-rb

### Debugging Gems
- pry-byebug: https://github.com/deivid-rodriguez/pry-byebug
- letter_opener: https://github.com/ryanb/letter_opener

### Coding Style Gems
- Rubocop: https://github.com/rubocop/rubocop
- Lefthook: https://github.com/evilmartians/lefthook

### Gems for Issues Tracking & Monitering
- Sentry: https://github.com/getsentry/sentry-ruby
- Honeybadger: https://github.com/honeybadger-io/honeybadger-ruby
- Bugsnag: https://github.com/bugsnag/bugsnag-ruby

### Google services
- Google API: [Documentation](https://googleapis.dev/ruby/google-api-client/v0.53.0/index.html) https://rubygems.org/gems/google-api-client 
- Google Drive: [Documentation](https://www.rubydoc.info/gems/google_drive/3.0.7) https://rubygems.org/gems/google_drive
    - Library for reading/writing files/spreadsheets in Google Drive/Documents.
- Google Auth: [Documentation](https://www.rubydoc.info/gems/googleauth/0.1.0) https://rubygems.org/gems/googleauth
    - Implements a simple authorization to access the Google APIs and provides support for default application credentials.

### Scraping & Parsing
- HTTParty: HTTP request gem https://github.com/jnunemaker/httparty
- Faraday: HTTP/REST API client library https://lostisland.github.io/faraday/usage/
- Nokogiri: Parsing gem https://github.com/sparklemotion/nokogiri
- Nikkou: Extract useful data from HTML and XML https://github.com/tombenner/nikkou 
- Mechanize: Automating interaction with websites https://github.com/sparklemotion/mechanize
