# MercadoPago SDK module for Payments integration

* [Install](#install)
* [Basic checkout](#basic-checkout)
* [Customized checkout](#custom-checkout)
* [Generic methods](#generic-methods)

<a name="install"></a>
## Install


### With Composer

From command line

```
composer require mercadopago/sdk:0.3.2
```

As a dependency in your project's composer.json

```json
{
    "require": {
        "mercadopago/sdk": "0.3.2"
    }
}
```

### By downloading

1. Clone/download this repository
2. Copy `lib/mercadopago.php` to your project's desired folder.

<a name="basic-checkout"></a>
## Basic checkout

### Configure your credentials

* Get your **CLIENT_ID** and **CLIENT_SECRET** in the following address:
    * Argentina: [https://www.mercadopago.com/mla/herramientas/aplicaciones](https://www.mercadopago.com/mla/herramientas/aplicaciones)
    * Brazil: [https://www.mercadopago.com/mlb/ferramentas/aplicacoes](https://www.mercadopago.com/mlb/ferramentas/aplicacoes)
    * Mexico: [https://www.mercadopago.com/mlm/herramientas/aplicaciones](https://www.mercadopago.com/mlm/herramientas/aplicaciones)
    * Venezuela: [https://www.mercadopago.com/mlv/herramientas/aplicaciones](https://www.mercadopago.com/mlv/herramientas/aplicaciones)
    * Colombia: [https://www.mercadopago.com/mco/herramientas/aplicaciones](https://www.mercadopago.com/mco/herramientas/aplicaciones)
    * Chile: [https://www.mercadopago.com/mlc/herramientas/aplicaciones](https://www.mercadopago.com/mlc/herramientas/aplicaciones)

```php
require_once ('mercadopago.php');

$mp = new MP ("CLIENT_ID", "CLIENT_SECRET");
```

### Preferences

#### Get an existent Checkout preference

```php
$preference = $mp->get_preference("PREFERENCE_ID");

print_r ($preference);
```

#### Create a Checkout preference

```php
$preference_data = array (
    "items" => array (
        array (
            "title" => "Test",
            "quantity" => 1,
            "currency_id" => "USD",
            "unit_price" => 10.4
        )
    )
);

$preference = $mp->create_preference($preference_data);

print_r ($preference);
```

#### Update an existent Checkout preference

```php
$preference_data = array (
    "items" => array (
        array (
            "title" => "Test Modified",
            "quantity" => 1,
            "currency_id" => "USD",
            "unit_price" => 20.4
        )
    )
);

$preference = $mp->update_preference("PREFERENCE_ID", $preference_data);

print_r ($preference);
```

### Payments/Collections

#### Search for payments

```php
$filters = array (
        "id"=>null,
        "site_id"=>null,
        "external_reference"=>null
    );

$searchResult = $mp->search_payment ($filters);

print_r ($searchResult);
```

#### Get payment data

```php
require_once ('mercadopago.php');

$mp = new MP ("CLIENT_ID", "CLIENT_SECRET");
$paymentInfo = $mp->get_payment ("PAYMENT_ID");

print_r ($paymentInfo);
```

#### Cancel (only for pending payments)

```php
$result = $mp->cancel_payment("PAYMENT_ID");

print_r ($result);
```

#### Refund (only for accredited payments)

```php
$result = $mp->refund_payment("PAYMENT_ID");

print_r ($result);
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

```php
require_once ('mercadopago.php');

$mp = new MP ("ACCESS_TOKEN");
```

### Create payment

```php
$mp->post ("/v1/payments", payment_data);
```

### Create customer

```php
$mp->post ("/v1/customers", array("email" => "email@test.com"));
```

### Get customer

```php
$mp->get ("/v1/customers/CUSTOMER_ID");
```

* View more Custom checkout related APIs in Developers Site
    * Argentina: [https://labs.mercadopago.com.ar/developers](https://labs.mercadopago.com.ar/developers)
    * Brazil: [https://labs.mercadopago.com.br/developers](https://labs.mercadopago.com.br/developers)
    * Mexico: [https://labs.mercadopago.com.mx/developers](https://labs.mercadopago.com.mx/developers)
    * Venezuela: [https://labs.mercadopago.com.ve/developers](https://labs.mercadopago.com.ve/developers)
    * Colombia: [https://labs.mercadopago.com.co/developers](https://labs.mercadopago.com.co/developers)

<a name="generic-methods"></a>
## Generic methods

You can access any resource from the MercadoPago API (https://api.mercadopago.com) using the generic methods:

```php
// Get a resource, with optional URL params. Also you can disable authentication for public APIs
$mp->get ("/resource/uri", [params], [authenticate=true]);

// Create a resource with "data" and optional URL params.
$mp->post ("/resource/uri", data, [params]);

// Update a resource with "data" and optional URL params.
$mp->put ("/resource/uri", data, [params]);

// Delete a resource with optional URL params.
$mp->delete ("/resource/uri", [params]);
```
