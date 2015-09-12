# Easy Captcha :)

[![Build Status](https://travis-ci.org/eusonlito/captcha.svg?branch=master)](https://travis-ci.org/eusonlito/captcha)
[![Latest Stable Version](https://poser.pugx.org/eusonlito/captcha/v/stable.png)](https://packagist.org/packages/eusonlito/captcha)
[![Total Downloads](https://poser.pugx.org/eusonlito/captcha/downloads.png)](https://packagist.org/packages/eusonlito/captcha)
[![License](https://poser.pugx.org/eusonlito/captcha/license.png)](https://packagist.org/packages/eusonlito/captcha)

A new simple and easy-to-implement captcha package.

## Installation with Composer

```json
{
    "require": {
        "eusonlito/captcha": "0.*"
    }
}
```

## Usage

### Template

```php
<?php use Eusonlito\Captcha\Captcha; ?>

<div class="form-group">
    <img src="<?= Captcha::source($LETTERS_COUNT, $WIDTH, $HEIGHT); ?>" class="img-responsive" />
    <input type="text" name="<?= Captcha::sessionName(); ?>" value="" class="form-control" />

    ... or ...

    <?= Captcha::img($LETTERS_COUNT, $WIDTH, $HEIGHT); ?>
    <input type="text" name="<?= Captcha::sessionName(); ?>" value="" class="form-control" />

    ... or ...

    <?= Captcha::img($LETTERS_COUNT, $WIDTH, $HEIGHT, array('class' => 'img-responsive')); ?>
    <input type="text" name="<?= Captcha::sessionName(); ?>" value="" class="form-control" />

    ... or ...

    <?= Captcha::img($LETTERS_COUNT, $WIDTH, $HEIGHT); ?>
    <?= Captcha::input(array('class' => 'form-control')); ?>

    ... or ...

    <?= Captcha::img(array($LETTERS_MIN, $LETTERS_MAX) $WIDTH, $HEIGHT); ?>
    <?= Captcha::input(array('class' => 'form-control')); ?>
</div>
```

If you are using an environment without sessions, you must add `Captcha::sessionStart()` before any html output (Controller).

### Checking

```php
<?php
use Eusonlito\Captcha\Captcha;

function validate()
{
    if (!Captcha::check()) {
        throw new Exception('Captcha text is not correct');
    }
}
```

That's all!

### Laravel Usage

```php
<?php
# config/app.php

return [
    ...

    'aliases' => [
        ...

        'Captcha' => 'Eusonlito\Captcha\Captcha',

        ...
    ]
];
```

Now you will have a `Captcha` class available on your controllers and views.

## Print Options

```php
<?php
use Eusonlito\Captcha\Captcha;

# Simple usage with fixed word length
Captcha::source($LETTERS_COUNT, $WIDTH, $HEIGHT); # Print base64 source image code

# Define min and max word length
Captcha::source(array($LETTERS_MIN, $LETTERS_MAX), $WIDTH, $HEIGHT); # Print base64 source image code

# Same using img tag
Captcha::img($LETTERS_COUNT, $WIDTH, $HEIGHT); # Print img tag
Captcha::img(array($LETTERS_MIN, $LETTERS_MAX), $WIDTH, $HEIGHT); # Print img tag

# Img tag with parameters
Captcha::img($LETTERS_COUNT, $WIDTH, $HEIGHT, array('class' => 'img-responsive')); # Print img tag with class attribute

# Simple input tag print
Captcha::input(); # Print input tag

# Input tag with parameters
Captcha::input(array('class' => 'form-control')); # Print input tag with class attribute
```

## Custom Setup

All custom settings will be defined before `img`, `source` or `check` methods calls.

```php
<?php
use Eusonlito\Captcha\Captcha;

# Define a unique font to use (only .ttf)
Captcha::setFont(__DIR__.'/../fonts/couture-bold.ttf'); # string or array

# Add fonts to repository (only .ttf)
Captcha::addFont(array(
    __DIR__.'/../fonts/couture-bold.ttf',
    __DIR__.'/../fonts/brush-lettering-one.ttf'
));

# Set custom rgb background
Captcha::setBackground(120, 120, 120); // Default is 255, 255, 255

# Set custom available letters
Captcha::setLetters('ABCDE3456'); // Default are 'ABCDEFGHJKLMNPRSTUVWXYZ'

# Set custom session name captcha storage (captcha string is stored crypted)
Captcha::sessionName('my-captcha'); // Default is 'captcha-string'

# Enable session before use on non session environments
Captcha::sessionStart();
```

Enjoy!