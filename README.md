# Lamb

Smallest Pure Functional Programming Language in C. Based on [Untype Lambda Calculus](https://en.wikipedia.org/wiki/Lambda_calculus) with Normal Order reduction.

> [!WARNING]
> The language currently does not have any memory management and leaks a lot of memory on each reduction. Garbage Collection will be implemented later.

## Quick Start

```console
$ cc -std=c99 -o lamb lamb.c
$ ./lamb
,---@.
 W-W'
Enter :help for more info
𝛌> (\f.(\x.f (x x)) (\x.f (x x))) g
(\f.(\x.f (x x)) (\x.f (x x))) g
(\x.g (x x)) (\x.g (x x))
g ((\x.g (x x)) (\x.g (x x)))
g (g ((\x.g (x x)) (\x.g (x x))))
g (g (g ((\x.g (x x)) (\x.g (x x)))))
g (g (g (g ((\x.g (x x)) (\x.g (x x))))))
g (g (g (g (g ((\x.g (x x)) (\x.g (x x)))))))
g (g (g (g (g (g ((\x.g (x x)) (\x.g (x x))))))))
g (g (g (g (g (g (g ((\x.g (x x)) (\x.g (x x)))))))))
g (g (g (g (g (g (g (g ((\x.g (x x)) (\x.g (x x))))))))))
...
```

It's recommended to use Lamb with [rlwrap](https://github.com/hanslub42/rlwrap). Just do

```console
$ rlwrap ./lamb
```

and you get Bash-style history and command line navigation.

## Syntax

The syntax is based on the [Notation of Untype Lambda Calculus](https://en.wikipedia.org/wiki/Lambda_calculus_definition#Notation) and provides few improvements over it.

### Variables

Variables are any alphanumeric names:

```
𝛌> x
x
𝛌> hello69
hello69
𝛌> 69420
69420
𝛌>
```

Yes, fully numeric sequences of characters are also considered names, because they are alphanumeric. This may change in the future.

### Functions

To denote functions instead of small greek almbda `𝛌` we use backslash `\` (this may change in the future, we are considering allowing `𝛌` as an alternative):

```
𝛌> \x.x
\x.x
𝛌> \x.\y.x
\x.\y.x
𝛌>
```

The body of the function extends as far right as possible. Use parenthesis to denote the boundaries of the function:

```
𝛌> \x.x x
\x.x x
𝛌> (\x.x) x
(\x.x) x
x
𝛌>
```

Since the variable names can be longer than 1 character we can't use that silly mathematician trick of stitching their names together by saying that `\xy.x` means `\x.\y.x`, because in Lamb it just means it's a single function with a parameter `xy`:

```
𝛌> \xy.x
\xy.x
𝛌> (\xy.x) z
(\xy.x) z
x
𝛌>
```

Instead we allow you to drop consequent backslashes turning the dot `.` into a parameter separator:

```
𝛌> \x.y.x
\x.\y.x
𝛌> (\x.y.x) z
(\x.\y.x) z
\y.z
𝛌>
```

## Applications

Just separate two lambda expressions with a space:

```
𝛌> (\x.x) x
(\x.x) x
x
𝛌>
```

You can drop parenthesis if the expression is unambiguous:

```
𝛌> f \x.x
f (\x.x)
𝛌>
```

Applications are left-associative:

```
𝛌> f a b c d
(((f a) b) c) d
𝛌>
```
