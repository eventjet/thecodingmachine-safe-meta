# thecodingmachine/safe Meta Package

## What is this?

This package is a small wrapper to allow installing [`thecodingmachine/safe`](https://github.com/thecodingmachine/safe)
on PHP 7 and [`thecodingmachine/safe8`](https://github.com/thecodingmachine/safe8) on PHP 8 automatically, depending on
the used PHP version.

## Why do I need this?

`thecodingmachine/safe` is only available for PHP 7. For PHP 8, `thecodingmachine/safe8` was created. That makes it
impossible to have a package using the awesome `Safe` library while supporting PHP `^7.4 || ^8.0`.

## How do I use it?

Instead of requiring `thecodingmachine/safe` directly, use this package in `composer.json`:

```json
{
    "require": {
        "php": "^7.4 || ^8.0",
        "eventjet/thecodingmachine-safe-meta": "^1.0 || ^2.0"
    }
}
```

## Caveats

Requiring a package indirectly introduces a _hidden dependency_, which is excatly what this package does. Therefore, if
you use [ComposerRequireChecker](https://github.com/maglnet/ComposerRequireChecker), it will complain. As a workaround
you have to whitelist every function/class that is used in your code.

Create a `require-checker.json` file which includes the used `Safe` functions:

```json
{
    "symbol-whitelist": [
        "null",
        "true",
        "false",
        "static",
        "self",
        "parent",
        "array",
        "string",
        "int",
        "float",
        "bool",
        "iterable",
        "callable",
        "void",
        "object",
        "mixed",

        "Safe\\sprintf"
    ]
}
```

And then run the checker with that config: `vendor/bin/composer-require-checker --config-file=require-checker.json`.

If you know a better workaround for that, please let me know!

## Thanks!

Special thanks goes to [Kharhamel](https://github.com/Kharhamel) and all contributors who
created `thecodingmachine/safe`!
Hopefully, some time this package won't be required anymore if there is some way for `Safe`
to support PHP 7 and PHP 8 in one package.
