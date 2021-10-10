# 🗾 Defining plans

Cashierstream is written on top of [Cashier Register](https://github.com/renoki-co/cashier-register), a complete plan and usage quota manager for your Laravel application.

The plans defined will be available for your users through the UI portal. You can follow the [Cashier Register examples](https://rennokki.gitbook.io/cashier-register/defining-plans/defining-the-plans) and leverage the true power of billing.

```php
use RenokiCo\CashierRegister\CashierRegisterServiceProvider as BaseServiceProvider;
use RenokiCo\CashierRegister\Saas;

class CashierRegisterServiceProvider extends BaseServiceProvider
{
    /**
     * Boot the service provider.
     *
     * @return void
     */
    public function boot()
    {
        parent::boot();

        Saas::plan('Gold Plan', 'price_xxx')
            ->monthly(30)
            ->features([
                Saas::feature('Seats', 'seats', 5)->notResettable(),
                Saas::feature('Projects', 'projects')->unlimited()->notResettable(),
            ]);
    }
}
```
