#### What is Stub?
A stub is also called a Method Stub. A special type of method that “stands in” for an existing method, or for a method that doesn't even exist yet.

For example, when testing a products controller and we are testing the list of 10 recent published products 

``````
describe ProductsController do
  describe "#index" do
    it "finds the 10 recent published products" do
      10.times { |i| create(:product, :published, title: "published_product_#{i}") }
      create(:product, published: false, title: "unpublished_product")

      get :index

      expect(assigns[:products].map(&:title)).to match_array(%w(
        published_product_0 published_product_1 published_product_2 published_product_3 published_product_4 published_product_5 published_product_6 published_product_7 published_product_8 published_product_9
      ))
    end
  end
end
``````
Issues within above example:
- The setup and verification phases become complex and hard to follow.
- We need to re-test the logic to find 10 published products, even though this logic is already implemented and tested in the model layer.

We can use stubs to clean it up:
- We can create test doubles in RSpec by using the double method:

``````
describe ProductsController do
  describe "#index" do
    it "finds the 10 recent published products" do
      products = double("latest_published")
      allow(Product).to receive(:latest_published).and_return(products)

      get :index

      expect(assigns[:products]).to eq(products)
    end
  end
end
``````
The products variable above is called a "stub," which is a kind of "test double."