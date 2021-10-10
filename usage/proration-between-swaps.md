# ⏱ Proration between swaps

By default, Billing Portal prorates the swap between plans. If you wish to not prorate the subscription between swaps, you can specify this in your service provider:

```php
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

        BillingPortal::dontProrateOnSwap();
    }
}
```
