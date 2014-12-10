# CodeIgniter-reCAPTCHA

The FREE anti-abuse service. Easy to add, advanced security, accessible to wide range of users and platforms. This package is compliant with [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md) and [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md).

# What is reCAPTCHA?

reCAPTCHA is a free service that protects your site from spam and abuse. It uses advanced risk analysis engine to tell humans and bots apart. With the new API, a significant number of your valid human users will pass the reCAPTCHA challenge without having to solve a CAPTCHA (See blog for more details). reCAPTCHA comes in the form of a widget that you can easily add to your blog, forum, registration form, etc.

See [the details][1].

# Sign up for an API key pair

To use reCAPTCHA, you need to [sign up for an API key pair][4] for your site. The key pair consists of a site key and secret. The site key is used to display the widget on your site. The secret authorizes communication between your application backend and the reCAPTCHA server to verify the user's response. The secret needs to be kept safe for security purposes.

# Installation

You can install via http://getsparks.org/packages/recaptcha-library/show

```bash
$ php tools/spark install -v1.0.2 recaptcha-library
```

or manual install

```bash
$ cp config/recaptcha.php your_application/config/
$ cp libraries/recaptcha.php your_application/libraries/
```

# Usage

Set your site key and secret on `config/recaptcha.php` file

```php
$config['recaptcha_site_key'] = '';
$config['recaptcha_secret_key'] = '';
```

### Render the reCAPTCHA widget

```php
$this->load->library('recaptcha');
echo $this->recaptcha->getWidget();
```

output:

```html
<div class="g-recaptcha" data-sitekey="xxxx" data-theme="light" data-type="image" data-callback="" ></div>
```

change default theme by pass array parameter

```php
echo $this->recaptcha->getWidget(array('data-theme' => 'dark'));
```

change default type by pass array parameter

```php
echo $this->recaptcha->getWidget(array('data-theme' => 'dark', 'data-type' => 'audio'));
```

### Render Script Tag

```php
$this->load->library('recaptcha');
echo $this->recaptcha->getScriptTag();
```

output:

```html
<script type="text/javascript" src="https://www.google.com/recaptcha/api.js?render=onload&hl=en" async defer></script>
```

change render value by pass array parameter

```php
echo $this->recaptcha->getScriptTag(array('render' => 'explicit'));
```

change default language by pass array parameter

```php
echo $this->recaptcha->getScriptTag(array('render' => 'explicit', 'hl' => 'zh-TW'));
```

### Verify Response

Calls the reCAPTCHA siteverify API to verify whether the user passes `g-recaptcha-response` POST parameter.

```php
$recaptcha = $this->input->post('g-recaptcha-response');
$response = $this->recaptcha->verifyResponse($recaptcha);
```

check success or fail

```php
if (isset($response['success']) and $response['success'] === true) {
    echo "You got it!";
}
```

see the [example controller](example/controller/test.php) and [view](example/views/recaptcha.php)

# Author

Bo-Yi Wu [@appleboy](https://twitter.com/appleboy)

[1]: https://www.google.com/recaptcha/intro/index.html
[2]: http://www.codeigniter.com/
[3]: https://developers.google.com/recaptcha/
[4]: http://www.google.com/recaptcha/admin
