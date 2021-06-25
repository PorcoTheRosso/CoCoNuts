ACME POS Terminal
=================

This is the code starter for the custom POS terminal our client, the ACME Germany GmbH, wants you to build.

The software will run on simple custom hardware.
It needs to take text input and produce text output.

To get started:

* Make *one* fork of this repository per team.
* Add all other team members to the forked repository.
* Every team member can now clone the forked repository & push to it.


Handling Money in Code
----------------------

Money can be tricky when programming.
Do not **ever** use `float` to represent money!
The code starter includes dedicated classes such as `Money` (an implementation of `MonetaryAmount`) for handling any product prices.

`MonetaryAmount`s are immutable!
Remember that when you try to compute prices.
See also the examples below.

Formatting of amounts of money can be achieved with a `MonetaryAmountFormat` like this:

```java
CurrencyUnit EUR = Monetary.getCurrency("EUR");
MonetaryAmount price1 = Money.ofMinor(EUR, 499);
MonetaryAmount price2 = Money.ofMinor(EUR, 1395);
MonetaryAmount total = price1.add(price2);
MonetaryAmountFormat format = MonetaryFormats.getAmountFormat(Locale.GERMANY);
String formattedAmount = format.format(total)
```

To round amounts of money correctly, use a `MonetaryRounding`. The following code rounds an amount of money to whole Euro cents:

``` java
CurrencyUnit EUR = Monetary.getCurrency("EUR");
MonetaryAmount price = Money.ofMinor(EUR, 1256);
MonetaryAmount total = price.multiply(BigDecimal.valueOf(119, 2));
MonetaryRounding rounding = Monetary.getRounding(RoundingQueryBuilder.of().setCurrency(EUR).set("cashRounding", true).build())
MonetaryAmount rounded = total.with(rounding);
```
