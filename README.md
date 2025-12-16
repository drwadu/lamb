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
λ> (\f.(\x.f (x x)) (\x.f (x x))) g
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

It's recommended to use Lamb with [rlwrap](https://github.com/hanslub42/rlwrap).
