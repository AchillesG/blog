# Starting Out

### simple arithmetic

``` Haskell
ghci> 2 + 15  -- 17
ghci> 49 * 100  -- 4900
ghci> 1892 - 1472  -- 420
ghci> 5 / 2  -- 2.5

ghci> (50 * 100) - 4999  -- 1
ghci> 50 * 100 - 4999  -- 1
ghci> 50 * (100 - 4999)  -- -244950
```

A little pitfall to watch out for here is negating numbers. If we want to have a negative number, it's always best to surround it with parentheses. Doing 5 * -3 will make GHCI yell at you but doing 5 * (-3) will work just fine.

>  注意负数的使用，负号紧挨操作符时 GHC 会报错。推荐的做法：使用负数时加上括号，如 (-3)。

Boolean algebra is also pretty straightforward. As you probably know, `&&` means a boolean _and_, `||` means a boolean _or_. `not` negates a `True` or a `False`.

``` Haskell
ghci> True && False  -- False
ghci> True && True  -- True
ghci> False || True  -- True
ghci> not False  -- True
ghci> not (True && True)  -- False
```

`&&` 布尔与，`||` 布尔或，`not` 布尔非

Testing for equality is done like so.

``` Haskell
ghci> 5 == 5  -- True
ghci> 1 == 0  -- False
ghci> 5 /= 5  -- False
ghci> 5 /= 4  -- True
ghci> "hello" == "hello"  -- True
```

> `==`, `/=` 是 Haskell 中判断相等的方法。

What about doing `5 + "llama"` or `5 == True`? Well, if we try the first snippet, we get a big scary error message!

``` Haskell
No instance for (Num [Char])
arising from a use of `+' at <interactive>:1:0-9
Possible fix: add an instance declaration for (Num [Char])
In the expression: 5 + "llama"
In the definition of `it': it = 5 + "llama"
```

> GHCI 告诉我们这里 `"llama"` 不是一个 number，所以它不知道怎么和 5 相加。甚至就算是 `"four"` 或者 `"4"`。`5 == True` 同理。

``` Haskell
ghci> succ 8  -- 9
```

> Haskell 中函数总是前缀形式的，并通过空格分隔函数名和参数以及参数和参数

``` Haskell
ghci> min 9 10 -- 9
ghci> min 3.4 3.2 -- 3.2
ghci> max 100 101 -- 101
```

Function application (calling a function by putting a space after it and then typing out the parameters) has the highest precedence of them all. What that means for us is that these two statements are equivalent.

``` Haskell
ghci> succ 9 + max 5 4 + 1 -- 16
ghci> (succ 9) + (max 5 4) + 1 -- 16
```

> 函数应用（通过在函数名后输入一个空格，并输入参数的方法来调用一个函数）在所有操作中拥有最高的优先级。所以，上面例子中的语句是等同的。于是，如果我们希望得到数字 9 和 10 的积的 successor，我们不能写 `succ 9 * 10`，而需要写 `succ (9 * 10)`。

If a function takes two parameters, we can also call it as an infix function by surrounding it with backticks.For instance,

``` Haskell
ghci> div 92 10 -- 9
ghci> 92 `div` 10 -- 9
```

> 如果一个函数接收两个参数，那么可以通过把它用``包起来，以中缀函数的形式调用它。

> 在 Haskell 中，区别于其他命令式函数通过括号调用函数的形式，采用空格来调用函数。因此 `bar (bar 3)` 类似于 C 语言中的 `bar(bar(3))`。

## Baby's first functions

``` Haskell
doubleMe x = x + x
```

Functions are defined in a similar way that they are called. The function name is followed by parameters seperated by spaces. But when defining functions, there's a `=` and after that we define what the function does.

> 函数的定义类似于调用。函数名后跟着由空格分隔的参数，但是在定义函数时，会需要一个额外的 =，并且在它之后定义函数的内容。

As expected, you can call your own functions from other functions that you made. With that in mind, we could define doubleUs like this:

``` Haskell
doubleUs x y = doubleMe x + doubleMe y
```

> 函数能够被别的函数调用。

> 上面是一个贯穿 Haskell 的通用模式的简单例子。它通过定义显然正确的基础函数，然后再将组合成一个更为复杂的函数。这也让你避免重复。

> Haskell 中的函数定义不需要按照顺序，可以先使用后定义。

``` Haskell
doubleSmallNumber x = if x > 100
                        then x
                        else x*2
```

Right here we introduced Haskell's if statement. The difference between Haskell's if statement and if statements in imperative languages is that the else part is mandatory in Haskell.

> Haskell 的 if 语句。与其他命令式语言 if 语句的区别在于 Haskell 的 else 部分是强制的。

Another thing about the if statement in Haskell is that it is an **expression**. An expression is basically a piece of code that returns a value. Because the else is mandatory, an if statement will always return something and that's why it's an expression. If we wanted to add one to every number that's produced in our previous function, we could have written its body like this.

> Haskell 中的 if 语句是一个**表达式**。表达式是指一段返回一个值的代码。因为 else 部分是必须的，所以 if 语句总是会返回一个值，这就是 if 语句是一个表达式的原因。如果你想为上个函数返回的值都加上 1，那么你可以这么写。

``` Haskell
doubleSmallNumber' x = (if x > 100 then x else x*2) + 1
```

That apostrophe doesn't have any special meaning in Haskell's syntax. It's a valid character to use in a function name. We usually use `'` to either denote a strict version of a function (one that isn't lazy) or a slightly modified version of a function or a variable.

> 撇号在 Haskell 语法中没有任何特殊意义，只是一个可以在函数名字中合法使用的字符。常使用 `'` 来代表一个函数的精确版本（不是惰性求值的），或者表示一个函数或变量的小修改版本。

``` Haskell
conanO'Brien = "It's a-me, Conan O'Brien!"
```

Because `'` is a valid character in functions, we can make a function like this. There are two noteworthy things here. The first is that in the function name we didn't capitalize Conan's name. That's because **functions can't begin with uppercase letters**. We'll see why a bit later. The second thing is that this function doesn't take any parameters. **When a function doesn't take any parameters, we usually say it's a definition (or a name)**. Because we can't change what names (and functions) mean once we've defined them, `conanO'Brien` and the string `"It's a-me, Conan O'Brien!"` can be used interchangeably.

> 1. 函数名必须以小写字母开头
> 2. 如果一个函数不需要参数，我们通常称其为定义（或名称）

> 因为不能修改定义好后的函数，所以 `conanO'Brien` 和字符串 `"It's a-me, Conan O'Brien!"` 可以相互替代使用。

## An intro to lists

In Haskell, lists are a **homogenous** data structure. It stores several elements of the same type.

> 在 Haskell 中，list 是同质的数据结构，它存储了几个相同数据类型的元素。

**Note**: We can use the `let` keyword to define a name right in GHCI. Doing `let a = 1` inside GHCI is the equivalent of writing `a = 1` in a script and then loading it.

> **注意**：在 GHCI 中可以使用 `let` 来定义。

``` Haskell
ghci> let lostNumbers = [4,8,15,16,23,42]
ghci> lostNumbers
[4,8,15,16,23,42]
```

字符串是字符的列表，`"hello"` 是 `['h','e','l','l','o']` 的语法糖。

通过 `++` 运算符来连接两个 list

``` Haskell
ghci> [1,2,3,4] ++ [9,10,11,12]
[1,2,3,4,9,10,11,12]
ghci> "hello" ++ " " ++ "world"
"hello world"
ghci> ['w','o'] ++ ['o','t']
"woot"
```

当对长列表使用 `++` 的时候需要注意，因为 `++` 的内部实现会将左侧的 list 遍历一次。

However, putting something at the beginning of a list using the `:` operator (also called the cons operator) is instantaneous.

> 通过 `:` 操作符（也被称为 cons 操作符）把元素添加到列表的开头则是瞬时的。

`[1,2,3]` is actually just syntactic sugar for `1:2:3:[]`. `[]` is an empty list. If we prepend `3` to it, it becomes `[3]`. If we prepend `2` to that, it becomes `[2,3]`, and so on.

> `[1,2,3]` 其实只是 `1:2:3:[]` 的语法糖。

``` Haskell
ghci> "Steve Buscemi" !! 6 -- 'B'
ghci> [9.4,33.2,96.2,11.2,23.25] !! 1 -- 33.2
```

可以使用 `!!` 通过 index 取出列表中的元素。

``` Haskell
ghci> [3,2,1] > [2,1,0] -- True
ghci> [3,2,1] > [2,10,100] -- True
ghci> [3,4,2] > [3,4] -- True
ghci> [3,4,2] > [2,4] -- True
ghci> [3,4,2] == [3,4,2] -- True
```

Lists can be compared if the stuff they contain can be compared. When using `<`, `<=`, `>` and `>=` to compare lists, they are compared in lexicographical order. First the heads are compared. If they are equal then the second elements are compared, etc.

> 如果一个列表包含的元素是可以比较的，那么这个列表也是可以比较的。当使用 `<`, `<=`, `>` 和 `>=` 比较列表时，是以字典顺序进行比较。

### list 常用函数

**`head`** takes a list and returns its head. The head of a list is basically its first element.

``` Haskell
ghci> head [5,4,3,2,1] -- 5
```

**`tail`** takes a list and returns its tail. In other words, it chops off a list's head.

``` Haskell
ghci> tail [5,4,3,2,1] -- [4,3,2,1]
```

**`last`** takes a list and returns its last element.

``` Haskell
ghci> last [5,4,3,2,1] -- 1
```

**`init`** takes a list and returns everything except its last element.

``` Haskell
ghci> init [5,4,3,2,1] -- [5,4,3,2]
```

![listmonster.png](https://i.loli.net/2018/05/25/5b07d881eb7b0.png)

When using `head`, `tail`, `last` and `init`, be careful not to use them on empty lists.
注意在空 list 上的使用。

**`length`** takes a list and returns its length, obviously.

**`null`** checks if a list is empty. If it is, it returns True, otherwise it returns False. Use this function instead of xs == [] (if you have a list called xs)

**`reverse`** reverses a list.

**`take`** takes number and a list. It extracts that many elements from the beginning of the list. Watch.

``` Haskell
ghci> take 3 [5,4,3,2,1] -- [5,4,3]
ghci> take 1 [3,9,3] -- [3]
ghci> take 5 [1,2] -- [1,2]
ghci> take 0 [6,6,6] -- []
```

See how if we try to take more elements than there are in the list, it just returns the list. If we try to take 0 elements, we get an empty list.\
当 `take` 的数量超过 list 长度的时候，直接返回 list 本身；如果 `take 0`，则返回空 list `[]`。

**`drop`** works in a similar way, only it drops the number of elements from the beginning of a list.

``` Haskell
ghci> drop 3 [8,4,2,1,5,6] -- [1,5,6]
ghci> drop 0 [1,2,3,4] -- [1,2,3,4]
ghci> drop 100 [1,2,3,4] -- []
```

**`maximum`** takes a list of stuff that can be put in some kind of order and returns the biggest element.

**`minimum`** returns the smallest.

**`sum`** takes a list of numbers and returns their sum.

**`product`** takes a list of numbers and returns their product.

**`elem`** takes a thing and a list of things and tells us if that thing is an element of the list. It's usually called as an infix function because it's easier to read that way.

``` Haskell
ghci> 4 `elem` [3,4,5,6] -- True
ghci> 10 `elem` [3,4,5,6] -- False
```

## Texas ranges

``` Haskell
ghci> [1..20] -- [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
ghci> ['a'..'z'] -- "abcdefghijklmnopqrstuvwxyz"
ghci> ['K'..'Z'] -- "KLMNOPQRSTUVWXYZ"
```

Ranges are cool because you can also specify a step.

``` haskell
ghci> [2,4..20] -- [2,4,6,8,10,12,14,16,18,20]
ghci> [3,6..20] -- [3,6,9,12,15,18]
```

You ***can't*** do `[1,2,4,8,16..100]` and expect to get all the powers of 2. **Firstly** because you can only specify one step. And **secondly** because some sequences that aren't arithmetic are ambiguous if given only by a few of their first terms.

To make a list with all the numbers from 20 to 1, you can't just do `[20..1]`, you have to do `[20,19..1]`.

Watch out when using **floating point** numbers in ranges! Because they are **not completely precise** (by definition), their use in ranges can yield some pretty funky results.

``` Haskell
ghci> [0.1, 0.3 .. 1]
[0.1,0.3,0.5,0.7,0.8999999999999999,1.0999999999999999]
```

My advice is ***not*** to use them in list ranges.

You can also use ranges to make infinite lists by just not specifying an upper limit. Later we'll go into more detail on infinite lists. For now, let's examine how you would get the first 24 multiples of 13. Sure, you could do `[13,26..24*13]`. But there's a better way: `take 24 [13,26..]`. Because Haskell is lazy, it won't try to evaluate the infinite list immediately because it would never finish. It'll wait to see what you want to get out of that infinite lists. And here it sees you just want the first 24 elements and it gladly obliges.

> 可以通过不给 range 设置上限来得到一个无限 list。\
> 对于获取前 24 个 13 的倍数，我们可以用 `[13,26..24*13]`，但更好的是用 `take 24 [13,26..]`。因为 Haskell 是惰性求值的，它不会立刻去计算一个无限 list，而是等到具体需要从无限 list 中取值时才计算。

生成无限 list 的函数

**`cycle`** takes a list and cycles it into an infinite list.

**`repeat`** takes an element and produces an infinite list of just that element. It's like cycling a list with only one element. Although it's simpler to just use the **`replicate`** function if you want some number of the same element in a list. `replicate 3 10` returns `[10,10,10]`.

## list comprehension

Mathematics: *set comprehensions*.\
A basic comprehension for a set that contains the first ten even natural numbers is ![setnotation.png](https://i.loli.net/2018/05/27/5b0ac583529ac.png)
. The part before the pipe is called the **output function**, x is the variable, `N` is the **input set** and `x <= 10` is the **predicate**. That means that the set contains the doubles of all natural numbers that satisfy the predicate.

List comprehensions are very similar to set comprehensions. The list comprehension we could use is `[x*2 | x <- [1..10]]`. `x` is drawn from `[1..10]` and for every element in `[1..10]` (which we have bound to `x`), we get that element, only doubled. Here's that comprehension in action.

``` Haskell
ghci> [x*2 | x <- [1..10]] -- [2,4,6,8,10,12,14,16,18,20]
```

**Predicates** go after the **binding** parts and are separated from them by a *comma(,)*.

``` Haskell
ghci> [x*2 | x <- [1..10], x*2 >= 12] -- [12,14,16,18,20]
```

Note that weeding out lists by predicates is also called **filtering**.

``` Haskell
boomBangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x]

ghci> boomBangs [7..13] -- ["BOOM!","BOOM!","BANG!","BANG!"]
```

Not only can we have multiple predicates in list comprehensions (an element must satisfy all the predicates to be included in the resulting list), we can also draw from several lists.

``` Haskell
ghci> [ x*y | x <- [2,5,10], y <- [8,10,11]] -- [16,20,22,40,50,55,80,100,110]

ghci> [ x*y | x <- [2,5,10], y <- [8,10,11], x*y > 50] -- [55,80,100,110]
```

Nested list comprehensions are also possible if you're operating on lists that contain lists.

``` Haskell
ghci> let xxs = [[1,3,5,2,3,1,2,4,5],[1,2,3,4,5,6,7,8,9],[1,2,4,2,1,6,3,1,3,2,3,6]]
ghci> [ [ x | x <- xs, even x ] | xs <- xxs]
[[2,2,4],[2,4,6,8],[2,4,2,6,2,6]]
```

## Tuples

Tuples are used when you know exactly how many values you want to combine and **its type depends on how many components it has and the types of the components**. They are denoted with parentheses and their components are separated by commas.

> Tuples 不必同质，但是内部元素的数量是固定的。Tuples 的类型和它内部元素的类型以及个数相关。

While there are *singleton lists*, there's **no** such thing as a *singleton tuple*. It doesn't really make much sense when you think about it. A singleton tuple would just be the value it contains and as such would have no benefit to us.

Like lists, tuples can be **compared** with each other if their components can be compared. Only you **can't** compare two tuples of **different sizes**, whereas you can compare two lists of different sizes.

Two useful functions that operate on pairs:

- **`fst`** takes a pair and returns its first component.

- **`snd`** takes a pair and returns its second component.

**`zip`**. It takes two lists and then zips them together into one list by joining the matching elements into pairs.

``` Haskell
ghci> zip [5,3,2,6,2,7,2,5,4,6,6] ["im","a","turtle"]
[(5,"im"),(3,"a"),(2,"turtle")]
```

Here's a problem that combines tuples and list comprehensions: which right triangle that has integers for all sides and all sides equal to or smaller than 10 has a perimeter of 24?

``` Haskell
ghci> let rightTriangles = [ (a,b,c) | c <- [1..10], b <- [1..c], a <- [1..b], a^2 + b^2 == c^2, a+b+c == 24]
ghci> rightTriangles
[(6,8,10)]
```
