# Gravatar for Laravel 5

## Installation

First, pull in the package through Composer via the command line:
```js
composer require creativeorange/gravatar
```

or add the following to your composer.json file and run `composer update`.

```js
"require": {
    "creativeorange/gravatar": "~1.0"
}
```

Then include the service provider within `app/config/app.php`.

```php
'providers' => [
    'Creativeorange\Gravatar\GravatarServiceProvider'
];
```

If you want to use the facade, add this to de bottom of `app/config/app.php`
And, for convenience, add a facade alias to this same file at the bottom:

```php
'aliases' => [
    'Gravatar' => 'Creativeorange\Gravatar\Facades\Gravatar',
];
```

Finally, publish the config by running the `php artisan vendor:publish` command


## Usage

Within your controllers or views, you can use

```php
    Gravatar::get('email@example.com');
```

this will return the URL to the gravatar image of the specified email address.
In case of a non-existing gravatar, it will return return a URL to a placeholder image. 
You can set the type of the placeholder in the configuration option `fallback`. 
For more infomation, visit http://en.gravatar.com/site/implement/images/#default-image

Alternatively, you can check for the existance of a gravatar image by using

```php
    Gravatar::exists('email@example.com');
```

This will return a boolean (`true` or `false`).

Or you can pass a url to a custom image using the fallback method:

```php
    Gravatar::fallback('http://urlto.example.com/avatar.jpg')->get('email@example.com');
```


## Configuration

You can create different configuration groups to use within your application and pass the group name as a second parameter to the `get`-method:
There is a default group in `config/gravatar.php` which will be used when you do not specify a second parameter.

If you would like to add more groups, feel free to edit the `config/gravatar.php` file. For example:

```php
return array(
	'default' => array(
		'size'   => 80,
		'fallback' => 'mm',
		'secure' => false,
		'maximumRating' => 'g',
		'forceDefault' => false,
		'forceExtension' => 'jpg',
	),
	'small-secure' => array (
	    'size'   => 30,
	    'secure' => true,
	),
	'medium' => array (
	    'size'   => 150,
	)
);
```

after that, you can use the following syntax:

```php
Gravatar::get('email@example.com', 'small-secure'); // will use the small-secure group
Gravatar::get('email@example.com', 'medium'); // will use the medium group
Gravatar::get('email@example.com', 'default'); // will use the default group
Gravatar::get('email@example.com'); // will use the default group
```


