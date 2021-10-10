# ⏫ Upgrading from 4.x

### Livewire

This version now has Livewire support thanks to [Atila Silva's Pull Request](upgrading-from-4.x.md#install-command).

### Install Command

Livewire was freshly introduced to this version and specifying the stack is no longer needed. The package will use the `jetstream.php`'s `stack` value to determine what to install, so it's important to install Jetstream and publish Jetstream assets before diving in and installing Cashierstream.

The command no longer needs the stack argument, so you can directly install the Cashier stack:

```bash
# Old behavior
php artisan billing-portal:install inertia stripe

# Current behavior
php artisan billing-portal:install stripe
```

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
