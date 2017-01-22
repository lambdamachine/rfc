# Common Λ

_CΛ_ &middot; _Common Lambda_ &middot; _Common Lambda Programming Language_

## Purpose

Define syntax of practical programming language based on [_Λ-calculus_](./lambda-calculus) system.

## Dependencies

Before reading this document, you should be familiar with:

* [_Λ-calculus_](./lambda-calculus)
* [_Combinatory logic_](./combinatory-logic)
* [_Sets_](./sets)

## CΛ vs. Λ-calculus

_Common Λ_ aims to be _Λ-calculus_ compatible. With the exception of [free variables](#free-variables), any valid _Λ-calculus_ expression shall be valid expression in _CΛ_.

### Free variables

For practical reasons, [free variables as in _Λ-calculus_](./lambda-calulus#free-variables) are not supported by _CΛ_. In order for a Λ-expression to be valid expression in _CΛ_, **all its variables must be bound**. In other words, **only combinators are valid expressions** in _CΛ_.

TODO: An image here would be awesome, something like road sign with description "only combinators allowed".

## Syntax

### Abstract syntax tree

Syntax of _common Λ_ expressions can be represented by an abstract tree with only three types of leafs - **variable**, **abstraction**, and **application**, as defined in our [formal definition of _Λ-calculus_](./lambda-calculus#formal-definition). We can define Λ-expression set as the following union:

```
Λ = Variables ∪ Abstractions ∪ Applications
```

Variable is a set of one element - a `name`. Theoretically, anything can be a variable name, thus we can describe it:

```
Variable = { 
  name ∈ ∞
}

Variables = {
  Variable,
  ...
}
```

Considering abstraction as `λarg.body`, we have a set of two elements - `arg` and `body` - being abstraction argument name and Λ-expression body, respectively. We can write it formally:

```
Abstraction = { 
  arg  ∈ Variables, 
  body ∈ Λ
}

Abstractions = { 
  Abstraction, 
  ...
}
```

Finally, considering application as `(fn arg)`, we have a set of two elements - this time `fn` and `arg` - respectively, function and applied argument. Written formally:

```
Application = { 
  fn  ∈ Λ, 
  arg ∈ Λ
}

Applications = {
  Application,
  ...
}
```

### Parser

TODO: describe checkpoints for implementing a parser.

## Related material

Hashtags:

* [**#commonlambda**](/hashtag/commonlambda)
