# MercadoPago SDK module for Payments integration

* [Install](#install)
* [Basic checkout](#basic-checkout)
* [Customized checkout](#custom-checkout)
* [Generic methods](#generic-methods)

<a name="install"></a>
## Install

```gem install mercadopago-sdk```

<a name="basic-checkout"></a>
## Basic checkout

### Configure your credentials

* Get your **CLIENT_ID** and **CLIENT_SECRET** in the following address:
    * Argentina: [https://www.mercadopago.com/mla/herramientas/aplicaciones](https://www.mercadopago.com/mla/herramientas/aplicaciones)
    * Brazil: [https://www.mercadopago.com/mlb/ferramentas/aplicacoes](https://www.mercadopago.com/mlb/ferramentas/aplicacoes)
    * México: [https://www.mercadopago.com/mlm/herramientas/aplicaciones](https://www.mercadopago.com/mlm/herramientas/aplicaciones)
    * Venezuela: [https://www.mercadopago.com/mlv/herramientas/aplicaciones](https://www.mercadopago.com/mlv/herramientas/aplicaciones)
    * Colombia: [https://www.mercadopago.com/mco/herramientas/aplicaciones](https://www.mercadopago.com/mco/herramientas/aplicaciones)
    * Chile: [https://www.mercadopago.com/mlc/herramientas/aplicaciones](https://www.mercadopago.com/mlc/herramientas/aplicaciones)

```ruby
require 'mercadopago-sdk'

mp = MercadoPago.new(CLIENT_ID, CLIENT_SECRET)
```

### Preferences

#### Get an existent Checkout preference

```ruby
preference = mp.preferences.find(preference_id)

puts preference
```

#### Create a Checkout preference

```ruby

params = {
  items: [
    {
      title: "T-Shirt",
      quantity: 1,
      unit_price: 10.2,
      currency_id: "ARS"
    }
  ]
}
preference = mp.preferences.create(params)

puts preference
```

#### Update an existent Checkout preference

```ruby
params = {
  items: [
    {
      title: "T-Shirt Updated",
      quantity: 1,
      unit_price: 2
    }
  ]
}

mp.preferences.update(preference_id, params)
```

### Payments/Collections

#### Search for payments

```ruby
filters = {
  site_id: AR
}

search_result = mp.payments.search(filters)

puts search_result
```

#### Get payment data

```ruby
payment = $mp.paymets.find(payment_id)

puts payment
```

### Cancel (only for pending payments)

```ruby
result = mp.payments.cancel(payment_id);
```

### Refund (only for accredited payments)

```ruby
result = mp.payments.refund(payment_id);
```

<a name="custom-checkout"></a>
## Customized checkout

### Configure your credentials

* Get your **ACCESS_TOKEN** in the following address:
    * Argentina: [https://www.mercadopago.com/mla/account/credentials](https://www.mercadopago.com/mla/account/credentials)
    * Brazil: [https://www.mercadopago.com/mlb/account/credentials](https://www.mercadopago.com/mlb/account/credentials)
    * Mexico: [https://www.mercadopago.com/mlm/account/credentials](https://www.mercadopago.com/mlm/account/credentials)
    * Venezuela: [https://www.mercadopago.com/mlv/account/credentials](https://www.mercadopago.com/mlv/account/credentials)
    * Colombia: [https://www.mercadopago.com/mco/account/credentials](https://www.mercadopago.com/mco/account/credentials)

```ruby
require 'mercadopago-sdk'

mp = MercadoPago.new(ACCESS_TOKEN)
```

### Create payment

```ruby
mp.post ("/v1/payments", payment_data);
```

### Create customer

```ruby
mp.post ("/v1/customers", { email: "email@test.com" })
```

### Get customer

```ruby
mp.get ("/v1/customers/#{customer_id}")
```

* View more Custom checkout related APIs in Developers Site
    * Argentina: [https://www.mercadopago.com.ar/developers](https://www.mercadopago.com.ar/developers)
    * Brazil: [https://www.mercadopago.com.br/developers](https://www.mercadopago.com.br/developers)
    * Mexico: [https://www.mercadopago.com.mx/developers](https://www.mercadopago.com.mx/developers)
    * Venezuela: [https://www.mercadopago.com.ve/developers](https://www.mercadopago.com.ve/developers)
    * Colombia: [https://www.mercadopago.com.co/developers](https://www.mercadopago.com.co/developers)

<a name="generic-methods"></a>
## Generic methods
You can access any other resource from the MercadoPago API using the generic methods:

```ruby
// Get a resource, with optional URL params. Also you can disable authentication for public APIs
mp.get ("/resource/uri", data, { authenticate: true })

// Create a resource with "data" and optional URL params.
mp.post ("/resource/uri", data, params)

// Update a resource with "data" and optional URL params.
mp.put ("/resource/uri", data, params)

// Delete a resource with optional URL params.
mp.delete ("/resource/uri", {}, params)
```

 For example, if you want to get the Sites list (no params and no authentication):

```ruby
sites = mp.get ("/sites")

puts sites
```
