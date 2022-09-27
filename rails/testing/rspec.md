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

#### What is Stub?
A stub is also called a Method Stub. A special type of method that “stands in” for an existing method, or for a method that doesn't even exist yet.

For example, when testing a products controller and we are testing the list of 10 recent published products 

Here is the example link where I explained more on "stub"