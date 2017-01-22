# Common Λ

_CΛ_ &middot; _Common Lambda_ &middot; _Common Lambda Programming Language_

## Purpose

Define syntax of practical programming language based on [_Λ-calculus_](./lambda-calculus) system.

## Dependencies

* [Λ-calculus](./lambda-calculus)
* [Combinatory logic](./combinatory-logic)
* [Functions](./functions)
* [Sets](./sets)
* [Parsers](./parsers)
* [Abstract syntax trees](./abstract-syntax-trees)

## CΛ vs. Λ-calculus

_Common Λ_ aims to be _Λ-calculus_ compatible. With the exception of [free variables](#free-variables), any valid _Λ-calculus_ expression shall be valid expression in _CΛ_.

### Free variables

For practical reasons, [free variables as in _Λ-calculus_](./lambda-calulus#free-variables) are not supported by _CΛ_. In order for a Λ-expression to be valid expression in _CΛ_, **all its variables must be bound**. In other words, **only combinators are valid expressions** in _CΛ_.

TODO: An image here would be awesome, something like road sign with description "only combinators allowed".

## Syntax

### Abstract syntax tree

Syntax of _common Λ_ expressions can be represented by an abstract tree with only three types of leafs - **variable**, **abstraction**, and **application**, as defined in our [formal definition of _Λ-calculus_](lambda-calculus-formal-definition). We can define Λ-expression set as the following union:

```
Λ = Variable ∪ Abstraction ∪ Application
```

Variable is a set of one element - a `name`. Theoretically, anything can be a variable name, thus we can describe it:

```
Variable = { 
  name ∈ ∞
}
```

Considering abstraction as `λarg.body`, we have a set of two elements - `arg` and `body` - being abstraction argument name and Λ-expression body, respectively. We can write it formally:

```
Abstraction = { 
  arg  ∈ Variable, 
  body ∈ Λ
}
```

Finally, considering application as `(fn arg)`, we have a set of two elements - this time `fn` and `arg` - respectively, function and applied argument. Written formally:

```
Application = { 
  fn  ∈ Λ, 
  arg ∈ Λ
}
```

### Scanner

A typical scanner of Λ-expressions should take single input - a rune reader - with `Rune` representating any single printable character. Such reader can be defined as an argumentless function returning single `Rune`: 

```
Reader = 𝑓 ⟶ Rune
```

A scanner must provide an interface to scan input streams of runes into recognized blocks. We can define scanner as a function from `Reader` to `Block`:

```
Scanner = 𝑓: Reader ⟶ Block
```

We can define block as well, with `String` representing any finite chain of runes:


```
Block = {
  token   ∈ Token,
  literal ∈ String
}
```

Only tokens are left to define. According to [formal definition of _Λ-calculus_](lambda-calculus-formal-definition), we have four special characters defining the notation, these are greek **lambda** `λ`, **dot** `.`, **left paren** `(` and **right paren** `)`. Naturally, two more standard tokens must be used. A **whitespace** token - matching all spaces, tabs and new lines - and of course **end of file** token. Everything else must be tokenized as **variable**.

Now, our tokens can be simply described as an enumerated set:

```
Token = { 
  EOF,
  LPAREN, 
  RPAREN, 
  LAMBDA, 
  DOT, 
  WHITESPACE, 
  VAR
}
```

### Parser

```
Parser = 𝑓: Reader ⟶ Λ ∪ ParserError

Trace = {
  position ∈ ℕ+
}

UnexpectedToken = {
  Trace,
  token ∈ Token
}

UnexpectedEndOfInput = {
  Trace
}

UnexpectedFreeVariable = {
  Trace,
  variable ∈ Variable
}

ParserError = {
  UnexpectedToken,
  UnexpectedEndOfInput,
  UnexpectedFreeVariable
}
```

TODO: describe checkpoints for implementing a parser.

## Related material

> HASHTAGS! [**#commonlambda**](/hashtag/commonlambda)

[lambda-calculus-formal-definition]: ./lambda-calculus#formal-definition
