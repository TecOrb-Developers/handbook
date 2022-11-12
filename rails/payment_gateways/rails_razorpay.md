# Razorpay Payment Gateway Integration

This codebase is interacting with the Razorpay API. This projects explains how to use Razorpay Payment Gatewat in our Rails Application.

## Link to Intrgration codebase
- [TecOrb-Developers/rails-razorpay-integration](https://github.com/TecOrb-Developers/rails-razorpay-integration)

## Required dependencies:

- Ruby is installed (v 3.1.0)
- Rails is installed (v 7.0.2)
- MySQL is installed
- Git is installed
- GitHub account is created
- Razorpay account created for business

## Major steps are followed to create and setup this project:
- Cloned/created a new rails project
- Database configuration setup (using MySQL)
- Initialize a local repository using git
- .gitignore file created to add configuration.yml
- configuration.yml file created to initialize environment variables
- Created a new remote repository using GitHub
- Implemented required APIs for order and process a payment
- Changed README.md and documentation added
- Code Commited and Pushed to GitHub repository

## Create configuration.yml to setup required environment variables
* Go to the config directory
* Create a new file with name *configuration.yml*

## Required variables to define in configuration.yml
````
RAZORPAY_KEY_ID:   payment_gateway_key_id
RAZORPAY_KEY_SECRET: payment_gateway_key_secret
````

## Used Gem
Payment Gateway
- ` gem 'razorpay'` here is the [link](https://github.com/razorpay/razorpay-ruby)

For authentication:
- Bcrypt here is the gem documentation [link](https://github.com/bcrypt-ruby/bcrypt-ruby)
- doorkeeper here is the gem documentation [link](https://github.com/doorkeeper-gem/doorkeeper)
- doorkeeper-jwt here is the gem documentation [link](https://github.com/doorkeeper-gem/doorkeeper-jwt)


## Implemented APIs Documentation

### 1. Signup User
User can signup by providing basic details
- Name
- Email 
- Password

### 2. Login User

```
    POST http://localhost:3000/oauth/token
```

| Request Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `email` | `string` | **Required**.  |
| `password` | `password_digest` | **Required**. |
| `client_id` | `string` | **Required**. |
| `client_secret` | `string` | **Required**. |
| `grant_type` | `string` | **Required**.  |


| Response Parameter | Type     | Response                |
| :-------- | :------- | :------------------------- |
| `access_token` | `string` | `eyJraWQiOiJxVTJERVIyREV***************`  |
| `token_type` | `string` | `Bearer` |
| `expires_in` | `integer` | `7200` |
| `refresh_token` | `string` | `yRUB93xdWSp8WP4hJd4AX***************` |
| `created_at` | `integer` | `166445***`  |


### 3. Order create
```
  POST http://localhost:3000/api/v1/order/create
 ```

| Request Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `amount` | `integer` | **Required**.  |
| `user_id` | `reference` | **Required**. |


| Response Parameter | Type     | Response                |
| :-------- | :------- | :------------------------- |
| `id` | `integer` | `1`  |
| `amount` | `integer` | `120` |
| `user_id` | `reference` | `2` |
| `gateway_order_id` | `string` | `yRUB93****` |


### 4.Make payment and verify
```
  POST http://localhost:3000/api/v1/order/verify
 ```

| Request Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `gateway_order_id` | `string` | **Required**.  |
| `razorpay_payment_id` | `string` | **Required**.  |
| `razorpay_signature` | `string` | **Required**.  |

| Response Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `status` | `boolean` |  `on success true` |
| `status` | `boolean` |  `on fails false` |


### Generate API Keys in Test and Live Modes, check error responses, parameters and other APIs.

```
  base_url = GET https://api.razorpay.com/v1
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `YOUR_KEY_ID` | `string` | **Required**. YOUR_KEY_ID |
| `YOUR_SECRET` | `string` | **Required**. Your YOUR_SECRET key |

### Test and Live Mode API Keys

```
  You can use Razorpay APIs in two modes, Test and Live. The API keys are different for each mode. Know about generating API Keys.
```

## Required dependencies to setup this project

- ruby v3.1.0
- rails v7.0.2

## Required data from Razorpay
We need to register our account on Razorpay as a business. We would need blow keys from our account:
- key_id
- key_secret

You can find your API keys at https://dashboard.razorpay.com/#/app/keys.

We will setup these keys in our Rozarpay configurations.
```
Razorpay.setup('key_id', 'key_secret')
```
### Razorpay features
Razorpay provides various features to manage the complete payment process for an order [link](https://razorpay.com/docs/api/basics).

Here is the list from their [documentation](https://github.com/razorpay/razorpay-ruby):
- Customer
- Token
- Order
- Payments
- Settlements
- Fund
- Refunds
- Invoice
- Plan
- Item
- Subscriptions
- Add-on
- Payment Links
- Smart Collect
- Transfer
- QR Code
- Emandate
- Cards
- Paper NACH
- UPI
- Register Emandate and Charge First Payment Together
- Register NACH and Charge First Payment Together
- Payment Verification
