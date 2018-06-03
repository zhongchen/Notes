# RegExp Notes

The [website](https://www.regular-expressions.info/reference.html) contains a lot of useful information.

The topic is so rich, but the fundamental idea is about two things

* Find the strings matching a pattern
* Achieve it in a high performance way

## Atomic Group

**(?>group)**

## Lazy Match

Place an extra **?**. Example: *?

## Possessive Quantifiers

Place an extra **+**. Example: ++, ?+, {n,m}+

Goal: improve performance by preventing the regex engine from trying all permutations.

## Non-capturing Group

(?:)