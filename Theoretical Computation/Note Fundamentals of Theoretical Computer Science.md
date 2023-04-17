# Fundamentals of Theoretical Computer Science

# Ch1. Preliminiaries

## 1.3 Alphabets and Strings

### Alphabet

An alphabet $A$ is a finte nonempty set, the element in $A$ is called symbols.

### String

An n-tuple of symbols of $A$ is a string, or word, on $A$.

### Language

The set of all strings on $A$ is the language of $A$, noted as $A^*$.

> For a word $u \in A$, define
>
> - $u^{[n]} := uu\cdots u$ for n numbers u.
> - $u^R$ is the reverse written of $u$.

## 1.4 Predicates

### Predicates

Predicates are special function maps from a set $S$ to $T/F$.

### Characteristic function

Considering a subset $R$ of $S$, which can be represented using the predicate as

$$R := \{x \in S | P(x)\}$$



> Note that the right part is the conditions the elements in this set should obey, thus the function P is called the [characteristic function](#characteristic-function).

## 1.5 Quantifiers(量词)

### Bounded existential quantifier

### Bounded universal quantifier

### De Morgan identities

## 1.7 Mathematical Induction

For some predicates claim on $N$, we need mathematical induction.

# 2. Programs and Computable Functions

## 2.1 A Formal Programmming Language in Turing Machine

Now, we define a formly programming language $\mathcal{L}$ using the concept of Turing Machines.

Considering certain letters as variables, to avoid the ambiguous of letter, we use $X_1, X_2, \cdots$ represente the variable, $Y$ as the output, $Z_i$ as the local variables of $\mathcal L$. And all the number variables are positive value and created with initial value 0.

A program instruction is some action written in a independent line, we can give any line a label.

A whole program in the language is some instructions list by line, and the machine can exist when it goto the label $E$ or after acting all the instructions.

Then the output $Y$ can be read by us.

A program in the programming language contains three action:

- Increase
  $X++$
- Decrease
  $X--$

  Especially if $X = 0$, leave it unchange, which may comes from the idea that the beginning of a calculation is definite.
- Goto
  IF $X \ne 0$ Goto L. When the condition is true, the machine can jump to the label L. 
  
  Actually, we can use the goto instructions with condition on some symbol X after the increase of X, which is always true, thus the Goto can represente the Loop with condition X.
  > Here, actually, the Turing Machine can backward to the beginning, then find the $L$ label and continue.

## 2.2 Basic example

### Example 1

Considering

$$f(x) \begin{cases}
    1 & x = 0\\
    x & otherwise\\
\end{cases}$$

can be represented by

```
[A]
X --
Y ++
IF X != 0 GOTO [A]
```
here, the only problem by these instruction is the initial value of $X$ can be zero, which means the output will be 1, as same as the output of $X = 1$.

### Example 2. Generate the GOTO keyword

Using a local variables can solve this problem. Here we introduces the local variables Z. The idea is
```
[A]
IF X != 0 GOTO Loop
EXIST

[Loop]
X --
Y ++

```

Here we use the condition with Z after its increase, which action of goto the exist.

```
[A] 
IF X != 0 GOTO [B]
Z ++
IF Z != 0 EXIST

[B] (Loop)
X --
Y ++
Z ++
```

Which means the instructions
```
Z ++
IF Z != 0 GOTO L
```
has the action of goto some label directly. Thus we define the GOTO instruction directly without ambiguous.

### Example 3. Copy of value.
Because all the variables just can increase or decrease. Considering a copy action as one is decreasing and the other is increasing. Thus we need a local variables to remeber the initial value of X.
```
COPY X TO Y, Z (then X is 0)
COPY Z TO X
```

with the program as

```
[A]
IF X != 0 GOTO B
GOTO C

[B]
X --
Y ++
Z ++
GOTO [A]

[C]
IF Z != 0 GOTO D
EXIST

[D](Copy back)
Z --
X ++
GOTO C
```

And these instruction of copy the value of V' to V is defined by macro as

```
V = V'
```

And local variable Z always has initial value 0 as it's just introduced in this local program. But the to be copied variable Y maybe not. So, all the instructions of copy a number to another just depend on the condition that the to be copied variable, the container, has the initial value zero. 

Thus add the initial value, we can always claim the COPY program is useful.

Here, we claim that all the labels, variables occur in the local program will not have repeat name with outer environment.

### Example 4. Add two number.
...
...
Then, we use the symbol "+" as the function.
### Example 5. Multiplies
...
...
Then, we use the symbol "*"

### Example 6. Loop

```
Y = X1
Z = X2
[C]
IF Z != 0 GOTO A

[A](Loop)
IF Y != 0 GOTO B
GOTO A

[B]
Y --
Z --
GOTO C
```


## 2.3 Syntax

This part is about the formally theory about outlanguage.

## 2.4 Computable Functions