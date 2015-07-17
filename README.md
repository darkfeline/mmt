# Missing macro tools for Emacs Lisp

[![License GPL 3](https://img.shields.io/badge/license-GPL_3-green.svg)](http://www.gnu.org/licenses/gpl-3.0.txt)
[![Build Status](https://travis-ci.org/mrkkrp/mmt.svg?branch=master)](https://travis-ci.org/mrkkrp/mmt)

The package contains classic tools for Emacs Lisp developers who want to
write macros with convenience.

The following functions and macros are present:

* `mmt-gensym`
* `mmt-with-gensyms`
* `mmt-with-unique-names`

## Installation

Put it on your `load-path` and then add the following at the top of file
where you would like to use the goodies:

```emacs-lisp
(require 'mmt)
```

That's it. Don't forget to include it in your list of dependencies if you
are writing an Emacs Lisp package:

```emacs-lisp
;; Package-Requires: ((emacs "24.1") (mmt "0.1.0"))
```

## API

```
mmt-gensym &optional x
```

Create and return new uninterned symbol as if by calling `make-symbol`.

The only difference between `mmt-gensym` and `make-symbol` is in how the new
symbol's name is determined. The name is concatenation of a prefix which
defaults to `"G"` and a suffix which is decimal representation of a number
that defaults to the value of `mmt--gensym-counter`.

If `x` is supplied and is a string, then that string is used as a prefix
instead of `"G"` for this call to `mmt-gensym` only.

If `x` is supplied and is an integer, then that integer is used instead of
the value of `mmt--gensym-counter` as the suffix for this call of
`mmt-gensym` only.

If and only if no explicit suffix is supplied `mmt--gensym-counter` is
incremented after it is used.

----

```
mmt-with-gensyms names &rest body
```

Bind each variable in `names` to a unique symbol and evaluate `body`.

Each of `names` must be either a symbol, or of the form:

```
(symbol string-or-symbol)
```

Bare symbols appearing in `names` are equivalent to:

```
(symbol symbol)
```

The `string-or-symbol` is used as the argument to `mmt-gensym` when
constructing the unique symbol the named variable will be bound to.

----

```
mmt-with-unique-names names &rest body
```

This is an alias for `mmt-with-gensyms`.

## License

Copyright © 2015 Mark Karpov

Distributed under GNU GPL, version 3.
