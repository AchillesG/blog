# Introduction

### Haskell is a _purely functional programming language_.

In imperative languages you get things done by giving the computer a sequence of tasks and then it executes them. While executing them, it can change state.

> 命令式语言通过给予计算机一个任务序列，并将之执行来完成工作。但是在执行任务序列过程中，命令式语言会改变环境的状态。

In purely functional programming you don't tell the computer what to do as such but rather you tell it what stuff _is_. You also can't set a variable to something and then set it to something else later.

> 在纯函数式语言中，你不需要告诉计算机去做什么，而是告诉计算机 _是什么_ 。并且，在为一个变量赋值后，你将不能再赋予它其他的值。

So in purely functional languages, a function has no side-effects. The only thing a function can do is calculate something and return it as a result.

> 所以在纯函数式语言中，函数没有副作用。函数唯一能做的只有计算和把结果返回。

At first, this seems kind of limiting but it actually has some very nice consequences: if a function is called twice with the same parameters, it's guaranteed to return the same result. That's called referential transparency and not only does it allow the compiler to reason about the program's behavior, but it also allows you to easily deduce (and even prove) that a function is correct and then build more complex functions by gluing simple functions together.

> 在开始，这似乎是一种限制，但实际上它拥有一些非常好的结果：如果一个函数以相同的参数被调用了两次，它能够保证函数也返回相同的结果。这被称为引用透明，这不但可以让编译器可以推断程序的行为，而且可以让你推断（甚至证明）一个函数是正确的，然后可以通过组合简单函数来构建更复杂的函数。

### Haskell is _lazy_.

That goes well with referential transparency and it allows you to think of programs as a series of transformations on data.

> Haskell 是惰性求值的，如无必要，不行求值。因为 Haskell 的引用透明性质惰性求值表现得很好，并且这让你将程序看作是 **数据的一系列变换** 。

### Haskell is _statically typed_.

That means that a lot of possible errors are caught at compile time. Haskell uses a very good type system that has type inference.

> Haskell 是静态类型的，这意味着很多错误可以在编译的时候发现。Haskell 的类型系统相当不错，支持类型推断。
