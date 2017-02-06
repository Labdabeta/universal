# Universal Scanner

## Table of Contents

 - [Overview](#overview)
 - [Language description](#language-description)

## Overview

The generation executable reads a definition of a lexical analyzer and outputs a
dfa file which can be loaded by the final compiler to correctly tokenize the
language.

## Language Description

The description file uses a very rudimentary regular expressions syntax to
define the various tokens that are valid. These regular expressions are then
processed into a deterministic finite automata which can be run via the maximal
munch algorithm to tokenize an input into tokens.

In this language the # character starts a comment until the end of the line.

The BNF of this language is:

```
DEFINITION ::=
    DEFINITION TOKEN_DEFINITION |
    TOKEN_DEFINITION
TOKEN_DEFINITION ::=
    NAME "is" ("valid")? REGEX ";"
REGEX ::=
    REGEX "|" REGEX |
    REGEX REGEX |
    REGEX* |
    REGEX+ |
    REGEX? |
    "(" REGEX ")" |
    LITERAL
LITERAL ::=
    SYMBOL |
    "[" SYMBOL+ "]" |
    "[^" SYMBOL+ "]" |
    """ NON_QUOTE+ """
NON_QUOTE ::=
    Any character except """
SYMBOL ::=
    Any character |
    "EOL"
```

Aside from literals whitespace is entirely ignored and merely used to separate
other valid tokens. The resulting lexer will only match the tokens marked as
valid and will match them with the precedence specified in the file by their
order.
