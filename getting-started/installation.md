# 🚀 Installation

### Setting up Jetstream

This package assumes you have installed Jetstream in your project. If not, head over to the [Jetstream website](https://jetstream.laravel.com) for installation steps.

### Installing Cashierstream

You can install the package via composer:

```bash
composer require renoki-co/jetstream-cashier-billing-portal
```

Next, publish the stubs, Laravel Cashier, Cashier Register, Cashierstream, and other related files for your choice:

```bash
php artisan billing-portal:install inertia stripe
```

### Installing Laravel Cashier

Make sure to have prepared your models to use Cashier as explained in the [Cashier documentation](https://laravel.com/docs/8.x/billing), including the billable traits and tables. Cashierstream will only install the appropriate packages in your composer file.

### Adding Stripe Checkout scripts

Cashierstream uses Stripe Checkout to ease the process of handling subscriptions.

You should do is to add the [Stripe Javascript SDK code](https://stripe.com/docs/js/including) **before** the `app.js` import in your `app.blade.php` file:

```markup
<script src="https://js.stripe.com/v3/"></script>
<script src="{{ mix('js/app.js') }}" defer></script>
```

### Setting up webhooks

Since Cashierstream uses Stripe Checkout, it's a must to have webhooks enabled so you can catch incoming subscriptions and modifications that happen in the Stripe Billing Portal.

Cashierstream already implements it for you. The default path is `/billing-portal/stripe/webhook` and you can modify it from the config file.

```bash
php artisan vendor:publish --provider="RenokiCo\BillingPortal\BillingPortalServiceProvider" --tag="config"
```

You will also need to specify the following events for the webhook in the Stripe Dashboard:

* `customer.subscription.created`
* `customer.subscription.updated`
* `customer.subscription.deleted`
* `customer.updated`
* `customer.deleted`
* `invoice.payment_action_required`
* `invoice.payment_succeeded`

Make sure you will also set the webhook secret env variable when running the app in production to better secure the exposed webhook endpoint:

```
STRIPE_KEY=stripe_key
STRIPE_SECRET=stripe_secret
STRIPE_WEBHOOK_SECRET=webhook_secret
```
