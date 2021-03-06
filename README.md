# Versus

Like [Ensure](https://github.com/SophieSpec/ensure), Versus is born with the thought that an ideal unit test should be a strict equality between the output of a function and its expected result. Versus enlarges Ensure tool so we can verify several inputs/ouputs with ease.

## Install

```sh
composer require --dev sophie-spec/versus
```

Requires PHP >= 7.4.

## Use

To test a method with several inputs/outputs, we simply pass the callable and yield values from a generator:

```php
use function Sophie\Versus\versus;

$add = function ($a, $b) {
    return $a + $b;
};

versus($add, function () {
    yield [1, 2] => 3;
    yield [-2, -3] => -5;
    yield [10, -20] => -10;
});
```

If the assertion fails, a `Sophie\Ensure\FailedAssertionException` error is thrown with a detailed message:

```php
versus($add, function () {
    yield [1, 2] => 100;
});
/*
    Both values are not equal.

    Provided value:
        3

    Expected value:
        100
*/
```

## License

[MIT](http://dreamysource.mit-license.org).
