# 🎎 Custom Billables

By default, the billing is made directly on the currently authenticated model. In some cases like using the billable trait on the Team model, you may change the model that will be retrieved from the current request.

You may define it in the `boot()` method of `BillingPortalServiceProvider`:

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

        BillingPortal::resolveBillable(function (Request $request) {
            return $request->user()->currentTeam;
        });
    }
}
```
