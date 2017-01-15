# Turing-Church Machine

TODO: Explain the concepts

> Why Turing-Church?

Because Turing Machine meets Alonzo Church's Lambda Calculus.

In a nutshell, _Turing-Church Machine_, or as we call it _Lambda Machine_, 
is an implementation of Turing Machine with infinite "Tape", 
programmable and optimized for lambda calculus.

## Purpose

Minimal general purpose environment for rapid software development.

---

Brief notes:

Turing envisioned I/O as an infinite tape, onto which values can be written and from which they can be read, in arbitrary order. In fact, the term *tape* is widely misunderstood. Tapes were in common use back in the 50's, thus Turing used the term as an example. Since the term is inaccurate and misconceptualized, it is better to use the term **space** instead. So as to Turing Machine vision, as he stated it, it consists of three parts:

1. Store
2. Executive Unit
3. Control

With *executive unit* being the part that carries individual instructions, where *control* ensures that instructions are executed correctly and in the right order. *Store* is the space, and control uses part of the space to carry with its purpose, usually by using table of instructions.

Now if we think about *space* and *control*, we might quickly find analogy to real world space-time relationship. In space-time, space is handles the physical storage, while time controls the access and order. Then really store and control are parts of the same thing, just as space and time has been proven to be parts of the same thing: *space-time*. We can then update definition of elements of Turing Machine with the following:

1. Space-Time
2. Executive Unit

Having this clarified, interesting questions start arising. If we consider Executive Unit to operate on Lambda Calculus, how such space time would be constructed? Should space and time properties be mapped to instructions or rather should they be implicitly handled by the nature of executive unit itself?

Consider an example lambda expression:

```
λget.(
  λset.(
    (set hello)world
    (get hello)
  )(
    λname.λvalue. ...
  )
)(
  λname. ...
)
```
 
That's how we could access the *space* from within lambda calculus, now considering previous question, another arises. Whether the `get` and `set` functions can be defined as pure lambda expressions or shall be provided by the underlying virtual machine. In other words, can lambda expression define *space-time* discretly and implicitly on top of execution unit, or execution unit must provide necessary primitives to let us access space?

The real question then is, can we create an execution unit that implicitly executes lambda expression, without need of I/O primitives at all?

Yet another question is if can this be done efficiently?

Lets see. Imagine lambda expressions as a tree.

```
λx.x
```

Execution tree for such expression can be drawn based on identity function.

```
input --> λx.x = input ? -- N --> x = input ? -- Y --> output
```

Since lambda calculus takes only one input and produces only one output, execution tree is binary. We can write execution tree of our identity funciton as binary then:

```
(λx.x) = 0
```

> Why 0?

Consider couple of examples:

```
(((λ x y z. x (y z))I)I)I      1
((λ y z. I (y z))I)I           1
(λ z. I (I z))I                1
I (I I)                        0
I I                            0
I                              0
      
111000

((λ x y . x)I)I   1
(λy.I)I           1
I I               0
I                 0

1100

((λ x y . x)I)I   1
(λy.y)I = I I     0
I                 0

100
```

This way we can effectively store any lambda expression in binary form.

TODO: Explain how this translates into building *space* and *space-time*
TODO: Explain how virtual machines can use pattern recognition instead of APIs to integrate with lambda machine. Point that pattern recognition of calculus execution can be considered output, and whenever input provided so far was insufficient to reach final identity, more input is expected to be provided.
