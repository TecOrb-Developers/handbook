## [Tecorb developers - RSpec](https://github.com/TecOrb-Developers/handbook/blob/main/rails/testing/rspec.md) / Mocks
### What are Mocks?
We use mocks to test the interaction between two objects. Instead of testing the output value, like in a regular expectation.

Here is an example of Mock. We are taking a class "Product" and one instance method "color"
````
class Product
  def color
    "green"
  end
end
````
For above, I am going to mock the Product model.
````
describe Product do
  context "fetching color of the product" do 
    before(:each) do
      @product = double("Product")
    end

    it "#color should return green" do
      allow(@product).to receive(:color).and_return("green")
      answer = @product.color
      expect(answer).to eq("green")
    end
  end
end

````

Where to use Mock and where not?
- If the method under test returns a value & it has no side effects (creating files, making API requests, etc.) **then you don’t need a mock**. Just check for the return value.
- If the method is working with external objects & sending orders to them, then you can mock the interactions with these objects.
- If the method is REQUESTING data from an external service (like an API), then you can use a stub to provide this data for testing purposes.

### References: 
- https://www.rubyguides.com/2018/10/rspec-mocks/
- https://semaphoreci.com/community/tutorials/mocking-with-rspec-doubles-and-expectations