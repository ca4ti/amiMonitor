# amiMonitor

This is a new colaboration of asterisk AMI with PHP. 

#### Donate
Help this project grow. Has many things to improve.
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate?business=3RVCDHAF83R4A&currency_code=USD)

# Instalation

## Via Composer just run `composer require ritch/ami-monitor` or clone this repository via Github.
## Run `composer install` if you cloned the project by git directly
## Run `npm install`


I Will improve this code and this explication, I swear, 
but if you only read this code, mainly `monitorManager.php` or run `php monitorManager.php`, You can use.

# Configuration

1) Copy the `config.ini.sample` to `config.ini` and put your configs

# To Run

1) If you want use web socket, run `node webSocketServer.js`, dont forget to put the configuration in `config.ini`.
2) Copy samples to your base directory `cp -rf vendor/ritch/ami-monitor/samples .` or make your self monitor.
3) Run `php samples/monitorManager.php`
3) Has a file `index.html` in samples folder, if you has using web socket, and all right, you'll start receive the events on your web page.

# Custom File monitor example:

```php
<?php 

namespace App;

//The path of autoload
include 'vendor/autoload.php';

use App\WebSocket;
use App\Ami;

set_time_limit(0);

$webSocket = new WebSocket();
$ami = new Ami();

//Filter some events or show All;
$event = [
	'All',
      /*'AgentLogin',
	'Hangup',
	'BridgeEnter',
	'AgentConnect',
	*/
];

do {
    switch ( @$amiEvent->Event ) {
	//If you has filtering some event, here you can do your logic, or send to websocket,
	case "Hangup":
		// You code here.
		$amiEvent = $ami->getEvent($event);
		$webSocket->emit( "MyCustomAction", [ $amiEvent ] );
		print_r($amiEvent);
	break;

	case "AgentConnect":
		// You code here.
	break;

	default:
		$amiEvent = $ami->getEvent($event);
		$webSocket->emit( "ami", [ $amiEvent ] );
		print_r($amiEvent);
	break;
     }
}
while ( Utils::check_asterisk_status() );

?>

```

# Donate
Help this project grow. Has many things to improve.

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate?business=3RVCDHAF83R4A&currency_code=USD)


