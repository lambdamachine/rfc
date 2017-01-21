# Common Lambda

## Purpose

Define syntax of common lambda calculus programming language supported by Lambda Machine.

## Formal definition

Lambda expressions are composed of:

* variables `v1`, `v2`, ..., `vn`, ...
* the abstraction symbols, greek lambda `λ` and dot `.`
* left `(` and right `)` parentheses

The set of lambda expressions, noted as capital greek lambda `Λ`, can be defined inductively:

#### Variables

If `x` is a variable then `x ∈ Λ`.

#### Applications

If `M, N ∈ Λ`, then `(M N) ∈ Λ`.

#### Lambda Abstractions

If `x` is a variable and `M ∈ Λ`, then `(λx.M) ∈ Λ`.

### Conventions

To keep the notation of lambda expressions uncluttered, the following conventions are usually applied:

* Outermost parentheses are dropped: `M N` is used instead of `(M N)`
* Applications are assumed to be left associative: `((M N) P)` may be written shortly as `M N P` 
* The body of an abstraction extends as far right as possible: `λx.M N` means `λx.(M N)` and not `(λx.M) N`
* A sequence of abstractions is contracted: sequence `λx.λy.λz.N` can be abbreviated as `λx y z.N`

> NOTE! In _common lambda_, expression `λx y z.N` is not the same as `λxyz.N`. The first one expands as `λx.λy.λz.N` while the other is just a single abstraction with an argument named `xyz`.

### Free and bound variables

In formal definition of _lambda calculus_, the abstraction operator, greek letter `λ`, is said to bind its variable wherever it occurs in the body of the abstraction. Variables that fall within the scope of an abstraction are said to be **bound**. All other variables are called **free**. For example, in the following expression `y` is a bound variable and `x` is free: `λy.x x y`. Also note that a variable is bound by its _nearest_ abstraction. The single occurrence of `x` in `λx.y (λx.z x)` is bound by the second lambda abstraction. An expression that contains no free variables is said to be **closed**. Closed lambda expressions are also known as **combinators** and are equivalent to **terms** in _combinatory logic_.

> IMPORTANT! Unlike in _lambda calculus_, in _common lambda_ **only combinators are allowed**. In other words, **all variables must be bound** in an expression for it to be valid _common lambda_ expression.

TODO: An image here would be awesome, something like road sign with description "only combinators allowed".

## Examples

TODO: Write few paragphs intro, something like lambda calculus for dummies. I want this document to be understood without walking out for extra resources. Examples should briefly explain what are combinators too.

## Syntax

### Abstract syntax tree

Syntax of _common lambda_ combinators can be represented by an abstract tree with only three types of leafs - **variable**, **abstraction**, and **application**, as defined in our [formal definition](#formal-definition).

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
