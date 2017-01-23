# Λ-calculus

## Formal definition

Lambda expressions, from now on called Λ-expression, are composed of:

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

To keep the notation of Λ-expressions uncluttered, the following conventions are usually applied:

* Outermost parentheses are dropped: `M N` is used instead of `(M N)`
* Applications are assumed to be left associative: `((M N) P)` may be written shortly as `M N P` 
* The body of an abstraction extends as far right as possible: `λx.M N` means `λx.(M N)` and not `(λx.M) N`
* A sequence of abstractions is contracted: sequence `λx.λy.λz.N` can be abbreviated as `λx y z.N`

> NOTE! Λ-expression `λx y z.N` is not the same as Λ-expression `λxyz.N`. The first one expands as `λx.λy.λz.N` while the other is just a single abstraction with an argument named `xyz`.

### Free and bound variables

The abstraction operator, greek letter `λ`, is said to bind its variable wherever it occurs in the body of the abstraction. Variables that fall within the scope of an abstraction are said to be **bound**. All other variables are called **free**. For example, in the following expression `y` is a bound variable and `x` is free: `λy.x x y`. Also note that a variable is bound by its _nearest_ abstraction. The single occurrence of `x` in `λx.y (λx.z x)` is bound by the second lambda abstraction. An expression that contains no free variables is said to be **closed**. Closed lambda expressions are also known as **combinators** and are equivalent to [**terms** in _combinatory logic_](./combinatory-logic#terms).

> HASHTAGS! #lambdacalculus
