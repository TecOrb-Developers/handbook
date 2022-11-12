## RSpec in BDD and TDD environments.
At Tecorb, we use RSpec tool to write tests for application features in most of the Ruby on Rails projects. TDD provides a novel and understandable way of writing tests that produces Test Driven Development even easier. 

Here are some of the benefits of using RSpec:
- TDD makes the code simpler and clear. It allows the developer to maintain less documentation.
- TDD prevents bugs in production, forces better code. 
- Encourages developers confidence when making changes to existing code bases.
- TDD promotes the development of high-quality code.

### How to test multi-step workflow in rspec
Best practices we follow for testing a multi-step workflow using rspec:
- define an object that creates the necessary state for each step and pass it forward for each successive one. 
- Basically we need to mock/stub the method calls for all the setup conditions

#### [What is Stub?](https://github.com/TecOrb-Developers/handbook/blob/main/rails/testing/stub.md)
A stub is also called a Method Stub. A special type of method that “stands in” for an existing method, or for a method that doesn't even exist yet.

For example, when testing a products controller and we are testing the list of 10 recent published products 

Here is the example where I explained more on ["stub"](https://github.com/TecOrb-Developers/handbook/blob/main/rails/testing/stub.md)

#### [What is a Mock?](https://github.com/TecOrb-Developers/handbook/blob/main/rails/testing/mock.md)
Mocking is the practice of using fake objects to mimic the behaviour of real application components. In other words mocking is a technique in test-driven development (TDD) that involves using fake objects or methods in order to write a test.

Here is the example where I explained more on ["Mock"](https://github.com/TecOrb-Developers/handbook/blob/main/rails/testing/mock.md)

##### What is the difference between Stub and Mock?
- A stub is only a method with a canned response, it doesn’t care about behavior.
- A mock expects methods to be called, if they are not called the test will fail.

### How to optimize & increase performance of RSpec tests
For our projects, we use dedicated CI (Continuous Integration) server bitbucket for running the full test suite. 

Here are the steps we follow to run the test suite:
- Developers make changes on a branch, commit, and push changes to bitbucket. 
- Then, create PR (Pull Request) regarding ticket.
- Then, bitbucket will pull down these changes and run the entire test suite.

#### Where Tests Performance matters?
A large code base when running the full test suite, it may takes 20+ minutes to run 2500+ tests. That will make us unproductive when we push changes and wait test suite to finish.

So the question is *How to increase the tests performance?*

Here are the solutions:

#### Separate Unit From Integration Tests

The first thing I would do is to separate unit from integration tests. We can do this either by:
- Moving them (into separate folders under the spec directory) - and modifying the rake targets
Tagging them *(rspec allows us to tag our tests)*
- Get our regular tests to run quick, and use a continuous integration server to run the more complete build. 

**Difference between integration tests and unit tests:**
- An integration test is a test that involves external dependencies (e.g. Database, WebService, Queue, and some would argue FileSystem). 
- A unit test just tests the specific item of code that we want checked. It should run fast (9000 in 45 secs is possible), i.e. most of it should run in memory.

#### Convert Integration Tests To Unit Tests
- If the most of our unit tests is smaller than our integration test suite, we have a problem. 
- What this means is that inconsistencies will begin to appear more easily. 
- So from here, start creating more unit tests to replace integration tests. 

*The points which we can follow in this process are:*
- Use a mocking framework instead of the real resource. Rspec has an inbuilt mocking framework.
- Run rcov on unit test suite. Use that to gauge how thorough unit test suite is.
- Once we have a proper unit test(s) to replace an integration test - remove the integration test.

#### Reduce the number of objects persisted to the database
- Instead of using build or create to instantiate your models with data, use build_stubbed.
- We use `gem 'factory_bot'` to build objects to the databse entities. Here is the [link](https://github.com/thoughtbot/factory_bot)

#### Don't Use Fixtures
- Fixtures are evil. Use a factory instead (machinist or factorybot)

#### Using Mock and stub when writting Tests specs
-  When we don't want an execute method that takes up time (like an API request or something), we can temporarily set a value it returns. 
- By stubbing methods on objects, we let them return a value which we set. 
- The methods are not called in this case, and the value is accessible for the asking.

#### Using Parallel Tests 
- Parallel Tests help us to reduce the run time of our test suite, resulting in faster build times and faster releases.
- We use `gem 'parallel_tests'` for parallel tests. Here is the [link](https://github.com/grosser/parallel_tests) for the gem on github

#### Database Cleaner configuration
- When we write ruby or rails code that interacts with a database and write unit test, chances are you have heard of or used the [database_cleaner gem](https://github.com/DatabaseCleaner/database_cleaner). 
- It's a terrific gem that abstracts away the various ORM APIs for getting the DB into a "blank slate" state. 
- Some setup needed to use it in optimal mode. 
- Here are some blogs that give us idea to setup [Blog 1](https://avdi.codes/configuring-database_cleaner-with-rails-rspec-capybara-and-selenium/) [Blog 2](https://medium.com/brief-stops/testing-with-rspec-factorygirl-faker-and-database-cleaner-651c71ca0688)

Configuring database_cleaner with Rails, Rspec, Capybara, and Selenium
Testing with Rspec, FactoryGirl, Faker and Database cleaner

### Popular gems used for testing:
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

[Check other gems we have worked with in our existing projects](https://github.com/TecOrb-Developers/handbook/blob/main/rails/used_gems.md)
