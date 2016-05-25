# Slack OAuth2 Provider for Laravel Socialite

## Documentation

This package makes use of the `SocialiteProviders` package located [here](http://socialiteproviders.github.io/).  
 
### Install the package

```sh
composer require mpociot/socialite-slack
```

### Install the Service Provider

* Remove `Laravel\Socialite\SocialiteServiceProvider` from your providers[] array in config\app.php if you have added it already.

* Add `\SocialiteProviders\Manager\ServiceProvider::class` to your providers[] array in config\app.php.


### Install the event listener

* Add `SocialiteProviders\Manager\SocialiteWasCalled` event to your listen[] array in `<app_name>/Providers/EventServiceProvider`.


* The listener that you add for this provider is `'Mpociot\Socialite\Slack\SlackExtendSocialite@handle',`.

For example:

```php
/**
 * The event handler mappings for the application.
 *
 * @var array
 */
protected $listen = [
    \SocialiteProviders\Manager\SocialiteWasCalled::class => [
        // add your listeners (aka providers) here
        'Mpociot\Socialite\Slack\SlackExtendSocialite@handle',
    ],
];
```

### Environment variables

If you add environment values to your `.env` as exactly shown below, you do not need to add an entry to the services array.

#### Append to .env

```
// other values above
SLACK_KEY=yourkeyfortheservice
SLACK_SECRET=yoursecretfortheservice
SLACK_REDIRECT_URI=https://example.com/login   
```

#### Append to config/services.php

You do not need to add this if you add the values to the `.env` exactly as shown above. The values below are provided as a convenience in the case that a developer is not able to use the .env method

```php
'slack' => [
    'client_id' => env('SLACK_KEY'),
    'client_secret' => env('SLACK_SECRET'),
    'redirect' => env('SLACK_REDIRECT_URI'),  
], 
```

## Usage

Redirect to Slack with the scopes you want to access:

```php
return Socialite::with('slack')->scopes([
	'identity.basic',
	'identity.email',
	'identity.team',
	'identity.avatar'
])->redirect();
```

## License

MIT :)