# Common Λ

_CΛ_, _Common Lambda_, _Common Lambda Programming Language_.

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

For practical reasons, [_free variables as in Λ-calculus_](./lambda-calulus#free-variables) are not supported by _CΛ_. In order for a Λ-expression to be valid expression in _CΛ_, **all its variables must be bound**. In other words, **only combinators are valid expressions** in _CΛ_.

TODO: An image here would be awesome, something like road sign with description "only combinators allowed".

## Syntax

### Abstract syntax tree

Syntax of _common Λ_ expressions can be represented by an abstract tree with only three types of leafs - **variable**, **abstraction**, and **application**, as defined in our [formal definition of _Λ-calculus_](./lambda-calculus#formal-definition). We can define Λ-expression set as a union:

```
Λ = Variable ∪ Abstraction ∪ Application
```

#### Variable

Stating the obvious, a variable is a set of one element - a `name`. Theoretically, anything can be a variable, thus we can describe it:

```
Variable = { 
  name ∈ ∞
}
```

#### Abstraction

Considering abstraction as `λarg.body`, we have a set of two elements - `arg` and `body` - being abstraction argument name and Λ-expression body, respectively. We can write it formally:

```
Abstraction = { 
  arg  ∈ Variable,
  body ∈ Λ
}
```

#### Application

Finally, considering application as `(fn arg)`, we have a set of two elements - this time `fn` and `arg` - respectively, function and applied argument. Written formally:

```
Application = {
  fn  ∈ Λ,
  arg ∈ Λ
}
```

### Parser

TODO: describe checkpoints for implementing a parser.

---

Syntax of Common Lambda expressio `E` can be generalised as folows:

```
E = ( v | λv.E | (E)E )
```

Examples of variables as in `E = v` are:

```
x
hello
(yada-yada-yada)
```

Examples of application as in `E = (E)E` are:

```
(x)y
(x((y)z))
(λx.x)(λx.λy.(x)y)
```

Examples of lambda abstractions as in `E = λv.E` are:

```
λx.y
λx.λy.x
(λx.(λy.(x)y)
```

### Currying

Common syntax supports currying:

```
λx.λy.λz.x y z = λ x y z . x y z
λx.x(λy.λz.x(y z)) = λx.x(λ y z . x (y z))
```

To improve readability, we allow curryied arguments to be separaded with comma:

```
λx,y,z.x y z
```

### Whitespaces

Whitespaces are to be ignored:

```
λ   x y   z   . ( x     y  z  ) = λ x y z . (x y z)
```

### Parentheses 

Most outer parens are optional:

```
(λx.(x x)) = λx.y z
(λx.(λy.((x)y)))) = λx.λy.(x)y = λx.λy.x y
```
