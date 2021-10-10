# ⏫ Upgrading from 4.x

###

### Authorization

You may configure the authorization validation for your users when accessing the portal. [Read the documentation about authorization](usage/authorization.md).

Make sure that the `config/billing-portal.php`'s `middleware` configuration adds the middleware needed for authorization:

```php
return [

    'middleware' => [
        // ...

        \RenokiCo\BillingPortal\Http\Middleware\Authorize::class,
    ],

    // ...
  
];
```

### Webhooks

Webhooks are already integrated with Cashierstream. The configuration was made to be flexible and change the path and the controller class used by the route. [Read more about the installation process for the webhooks ↗](getting-started/installation.md#setting-up-webhooks)

Append the following config to `config/billing-portal.php.`

```php
<?php

return [

    // ...
    
    /*
    |--------------------------------------------------------------------------
    | Webhook Controller
    |--------------------------------------------------------------------------
    |
    | The router settings for the webhook endpoints.
    | This is being prefixed by the prefix key that was configured above.
    |
    */
    
    'webhooks' => [

        'middleware' => [
            //
        ],


        'stripe' => [

            'path' => '/stripe/webhook',

            'class' => \RenokiCo\BillingPortal\Http\Controllers\StripeWebhook::class,

        ],

    ],
];
```
