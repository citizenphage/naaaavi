# naaaavi
Naming avoiding ambiguity automatically assigning valid identifiers


## What is it?

`Naaaavi` (pronounced `nah-vee` as if someone hadn't injected a load of ambiguous confusing `a` characters) is a simple Python tool for generating identifiers.
It attempts to generate identifiers that:

* use a character set (or other system) that aims to be human-friendly
* can be checksummed
* avoid ambiguity by testing the identifier against several `rejectors`
* are somewhat chronologically sortable
* are generated in a predictable fashion

It generates human-friendly identifiers using `diceware` (soon) or the `zbase32` alphabet, and allows for screening of common sources of confusion such as look-alike pairs and repetitive characters. `Naaaavi` also provides limited support for generating `ZPL` to print your nice new barcodes.

## What is it not?

`Naaaavi` does not:

* randomly generate identifiers
* encode anything into the identifiers
* generate universally or globally unique identifiers


## How do I use it?

### Generate barcodes

    $ naaaavi generate --alphabet zbase32 --checksum luhn_mod_n --size 6 --rejectors max_repeats:2 -n 10 --upper --prefix 'HOOT-'
    HOOT-YYBYBY     6       zbase32 luhn_mod_n      max_repeats=['2']       0.1.0

### Validate barcodes

    $ naaaavi validate --alphabet zbase32 --checksum luhn_mod_n --barcodes HOOT-YYBYBY.6 HOOT-YYBYBY6 YYBYBY6 YYBXBY6 YYBYBY7
    HOOT-YYBYBY.6   1
    HOOT-YYBYBY6    1
    YYBYBY6 1
    YYBXBY6 0
    YYBYBY7 0

## Rejectors

* `max_repeats` will reject any identifier which repeats a particular symbol more than `n` times consecutively
* `min_unique` will reject any identifier that does not have at least `n` unique characters
* `ismp_flips` will reject any identifier that has at least one look alike pair noted as potentially confusing by the Institute for Safe Medication Practices
* `ban_list` will reject any identifier that has a prefix or suffix in your list
* `regex_list` will reject any identifier that searches positive against a list of regular expressions
* `better_profanity` (requires `pip install better_profanity`) will overzealously reject any identifier that could be mildly amusing

## Notes

### I don't like your funny command name

The `navi` command is provided as a synonym of `naaaavi` so you don't have to remember that there are currently four `a` characters in `naaaavi`.
