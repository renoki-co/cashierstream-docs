# 💂‍♂️ Authorization

Cashierstream lets you define a custom closure to check whether the billable is allowed to perform a request on the billing portal.

The first thing you need to make sure of is to have the `RenokiCo\BillingPortal\Http\Middleware\Authorize` middleware in `config/billing-portal.php`:

```php
return [

    'middleware' => [
        // ...

        \RenokiCo\BillingPortal\Http\Middleware\Authorize::class,
    ],

    // ...
  
];
```

To customize the authorization response, you can define the closure resolver in your `BillingPortalServiceProvider` file:

```php
use Illuminate\Http\Request;
use RenokiCo\BillingPortal\BillingPortal;

class BillingPortalServiceProvider extends BaseServiceProvider
{
    /**
     * Boot the service provider.
     *
     * @return void
     */
    public function boot()
    {
        parent::boot();

        BillingPortal::resolveAuthorization(function ($billable, Request $request) {
            return $billable && $billable->id == $request->user()->id;
        });
    }
}
```

### Redirecting instead of throwing error

Based on the true/false return value, it will either allow the request to pass through or throw a 403 error response. However, you can redirect your users instead of letting the package throw the error. The package middleware will check for a `RedirectResponse` value and in case it is met, it will redirect the user instead of throwing the error:

```php
use Illuminate\Http\Request;
use RenokiCo\BillingPortal\BillingPortal;

class BillingPortalServiceProvider extends BaseServiceProvider
{
    /**
     * Boot the service provider.
     *
     * @return void
     */
    public function boot()
    {
        parent::boot();

        BillingPortal::resolveAuthorization(function ($billable, Request $request) {
            $isAuthorized = $billable && $billable->id == $request->user()->id;
            
            if (! $isAuthorized) {
                return Redirect::route('home')
                    ->with('flash.banner', 'You are not allowed to manage the subscriptions.')
                    ->with('flash.bannerStyle', 'danger');
            }
            
            return true;
        });
    }
}
```
