# 🚦 Routes

Cashierstream applies automatically the routes needed for your users to interact with their plans, invoices, and payment methods.

You can find a list with the applied routes file in [routes/inertia.php](https://github.com/renoki-co/jetstream-cashier-billing-portal/blob/master/routes/inertia.php).

```markup
<a href="{{ route('billing-portal.dashboard') }}">
    To the billing dashboard
</a>
```

Additionally, you may call the `route:list` command in your application:

```bash
$ php artisan route:list --compact | grep billing

| GET|HEAD      | billing                                             | RenokiCo\BillingPortal\Http\Controllers\Inertia\BillingController@dashboard                        |
| GET|HEAD      | billing/invoice                                     | RenokiCo\BillingPortal\Http\Controllers\Inertia\InvoiceController@index                            |
| GET|HEAD      | billing/payment-method                              | RenokiCo\BillingPortal\Http\Controllers\Inertia\PaymentMethodController@index                      |
| POST          | billing/payment-method                              | RenokiCo\BillingPortal\Http\Controllers\Inertia\PaymentMethodController@store                      |
| GET|HEAD      | billing/payment-method/create                       | RenokiCo\BillingPortal\Http\Controllers\Inertia\PaymentMethodController@create                     |
| GET|HEAD      | billing/payment-method/{payment_method}             | RenokiCo\BillingPortal\Http\Controllers\Inertia\PaymentMethodController@show                       |
| DELETE        | billing/payment-method/{payment_method}             | RenokiCo\BillingPortal\Http\Controllers\Inertia\PaymentMethodController@destroy                    |
| POST          | billing/payment-method/{payment_method}/set-default | RenokiCo\BillingPortal\Http\Controllers\Inertia\PaymentMethodController@setDefault                 |
| GET|HEAD      | billing/portal                                      | RenokiCo\BillingPortal\Http\Controllers\Inertia\BillingController@portal                           |
| GET|HEAD      | billing/subscription                                | RenokiCo\BillingPortal\Http\Controllers\Inertia\SubscriptionController@index                       |
| POST          | billing/subscription/cancel                         | RenokiCo\BillingPortal\Http\Controllers\Inertia\SubscriptionController@cancelSubscription          |
| POST          | billing/subscription/resume                         | RenokiCo\BillingPortal\Http\Controllers\Inertia\SubscriptionController@resumeSubscription          |
| POST          | billing/subscription/subscribe/{plan}               | RenokiCo\BillingPortal\Http\Controllers\Inertia\SubscriptionController@redirectWithSubscribeIntent |
| POST          | billing/subscription/swap/{plan}                    | RenokiCo\BillingPortal\Http\Controllers\Inertia\SubscriptionController@swapPlan                    |
```

All route names are prefixed with `billing-portal.` and you may change the prefix and middleware via `config/billing-portal.php`:

```bash
php artisan vendor:publish --provider="RenokiCo\BillingPortal\BillingPortalServiceProvider" --tag="config"
```
