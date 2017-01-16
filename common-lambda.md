# Common Lambda

## Purpose

Define syntax of common lambda calculus programming language supported by Lambda Machine.

## Syntax

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
