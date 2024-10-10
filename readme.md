
## Laravel MT5

This is Laravel 6.x package wrapper library for Metatrader 5 Web API
- [Official MT5 Web Api Documentation](https://support.metaquotes.net/en/docs/mt5/api/webapi).


## Documentation

### Installing 
To install the package, in terminal:
```
composer require PabloMazurkiewicz/LaravelMt5
```

### Configure
If you don't use auto-discovery, add the ServiceProvider to the providers array in config/app.php
```
PabloMazurkiewicz\LaravelMt5\LaravelMt5Provider::class,
```

#### Copy the package config to your local config with the publish command:

```bash
php artisan vendor:publish --provider="PabloMazurkiewicz\LaravelMt5\LaravelMt5Provider"
```

and then you can configure connection information to MT5 with this ``.env`` value

```dotenv
MT5_SERVER_IP=
MT5_SERVER_PORT=
MT5_SERVER_WEB_LOGIN=
MT5_SERVER_WEB_PASSWORD=
```

## Usage

### Create Deposit
```php
use PabloMazurkiewicz\LaravelMt5\Entities\Trade;
use PabloMazurkiewicz\LaravelMt5\LaravelMt5;

$api = new LaravelMt5();
$trade = new Trade();
$trade->setLogin(6000189);
$trade->setAmount(100);
$trade->setComment("Deposit");
$trade->setType(Trade::DEAL_BALANCE);
$result = $api->trade($trade);
```

The result variable will return Trade class with ticket information, you can grab ticket number by calling ``$result->getTicket()``

### Create User
```php
use PabloMazurkiewicz\LaravelMt5\Entities\User;
use PabloMazurkiewicz\LaravelMt5\LaravelMt5;

$api = new LaravelMt5();
$user = new User();
$user->setName("John Due");
$user->setEmail("john@due.com");
$user->setGroup("demo\demoforex");
$user->setLeverage("50");
$user->setPhone("11111111");
$user->setAddress("Cordoba");
$user->setCity("Cordoba");
$user->setState("Cordoba");
$user->setCountry("Argentina");
$user->setZipCode(1470);
$user->setMainPassword("Secure123");
$user->setInvestorPassword("NotSecure123");
$user->setPhonePassword("NotSecure123");

$result = $api->createUser($user);
```

### Get Trading Account Information
```php
use PabloMazurkiewicz\LaravelMt5\LaravelMt5;

$api = new LaravelMt5();
$user = $api->getTradingAccounts($login);

$balance = $user->Balance;
$equity = $user->Equity;
$freeMargin = $user->MarginFree;
```

### Get Trading History By Login Number
```php
use PabloMazurkiewicz\LaravelMt5\LaravelMt5;

$api = new LaravelMt5();
// Get Closed Order Total and pagination
$total = $api->getOrderHistoryTotal($exampleLogin, $timestampfrom, $timestampto);
$trades = $api->getOrderHistoryPagination($exampleLogin, $timestampfrom, $timestampto, 0, $total);
foreach ($trades as $trade) {
    // see class MTOrder
    echo "LOGIN : ".$trade->Login.PHP_EOL;
    echo "TICKET : ".$trade->Order.PHP_EOL;
}
```

### Open Order
```php
use PabloMazurkiewicz\LaravelMt5\LaravelMt5;
$api = new LaravelMt5();
$api->dealerSend([
    'Login' => 8113,
    'Symbol' => 'XAUUSD',
    'Volume' => 100,
    'Type' => 0
});
```



The result variable will return User class with login information, you can grab login number by calling ``$result->getLogin()``

### Todo

- [x] Deposit or Withdrawal
- [x] Create Account
- [x] Open Order
- [x] Get Trading Account Information
- [ ] Change Password
- [ ] Create Group
- [ ] Delete Group
- [ ] Get Accounts
- [ ] Remove Account
- [ ] Get Trades
- [ ] Get Group
   
## Contributing

Thank you for considering contributing to the Laravel MT5! you can fork this repository and make pull request.