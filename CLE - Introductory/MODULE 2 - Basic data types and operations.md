##  Numeric types 

The difference between a double and a int is so trivial I decided not to write it here, but essentially `int` refer to those whole positive or negative numbers while `float` represent the decimal, floating-point numbers.

`double` is _double_ the size of a `float` (the size of `float` is 4 bytes, while the size of `double` is 8 bytes), which means `double` has higher precision than `float`, but it also takes up more memory and is slower.

The variables of type `double` may differ from the variables of type `float`, not only in **range**, but also in **accuracy**. The data stored in a floating-point variable has **finite precision** – in other words, only a certain number of digits are **precisely stored** in the variable: We say that the variable saves (only) **8 precise digits**. This is within the expected accuracy of 32-bit long `float`s. Using a `double` (which is usually 64 bits long) guarantees that the variable will save a more significant number of digits – about **15-17**. This is where the name `double` comes from – its accuracy is **doubled** compared to `float`.

Exponential in scientific notation may be written as `XEY`, representing **X • 10^Y** . The letter _E_ (you can also use the lower case letter _e_ – it comes from the word exponent) is a concise version of the phrase “_times ten to the power of_”.

Note:

- the exponent (the value after the “_E_”) **must** be an integer.
- the base (the value in front of the “_E_”) **can** be an integer. 

Integers values can be forced into float values and vice-versa, however, when translating float to int, the decimal information is lost.

Also, they cannot contain arbitrarily large (or arbitrarily small) numbers. Most of the computers currently in use store `int`s using **32 bits** (4 bytes); this means that we can operate the `int`s within the range of [-2147483648 .. 2147483647]

If those limits are surpassed, the variable will be unable to store such a large value, but it isn’t clear what will happen during the assignment. Certainly, a **loss of accuracy** will occur, but the value assigned to the variable is not known in advance. In some systems, it may be the maximum permissible _int_ value, while in others an error occurs, and in others still the value assigned may be completely random.

This is what we call an **implementation dependent issue**. It's the second (and uglier) face of **software portability**.

The “C” language provides some methods for defining precisely how we intend to store large/small numbers. This allows the compiler to allocate memory, either smaller than usual (e.g. 16 bits instead of 32) or larger than usual (e.g. 64 bits instead of 32). We can also declare that we guarantee that the value stored in the variable will be **non-negative**.

In this case the width of the variable’s **range does not change**, but is **shifted** toward the positive numbers. This means that instead of the range of -2,147,483,648 .. 2,147,483,647 we get the range of 0 .. 4294967295.

To specify our memory requirements, we can use some additional keywords called **modifiers**:

- _long_ – is used to declare that we need a wider range of `int`s than the standard one;
- _short_ – is used to determine that we need a narrower range of `int`s than the standard one;
- _unsigned_ – is used to specify that a variable is needed only for non-negative numbers; 

Note that some compilers may not be able to distinguish data of type int and long. They may be synonyms. If you want to force the compiler to use actual long representation for a specific number, you can use the long long type.

Modifiers must not be used simultaneously in a single declaration.

So far we’ve used integer literals, assuming that all of them are of type `int`. This is generally the case, but there are some cases when the compiler recognizes literals of type `long`. This will happen if:

- a literal value goes **beyond the acceptable** range of type `int`;
- **letter L or l is appended** to the literal, such as `0L` or `1981l` – both of these literals are of type `long`.

Finally, the _short_ modifier nor the _unsigned_ cannot be used alongside the `float`, but we may use the _long_ modifier here. It’s assumed that type `long float` is a synonym for `double`. 

## Char

To store and manipulate characters, the “C” language provides a special type of data. This type is called a **char**, which is an abbreviation of the word _character_.

### ASCII
Computers store characters as numbers. Every character used by a computer corresponds to a unique number, and vice versa. This system of assignments includes more characters than you would probably expect. Many of them are invisible to humans but essential for computers.

Some of these characters are called **white spaces**, while others are named **control characters**, because their purpose is to **control** the input/output devices. An example of a white space that is completely invisible to the naked eye is a special code, or a pair of codes (different operating systems may treat this issue differently), which are used to mark the ends of lines inside text files. People don’t see this sign (or these signs), but they can see their effect where the lines are broken.

We can create virtually any number of assignments, but a world in which each computer type uses different character encoding would be extremely inconvenient. This has created a need to introduce a universal and widely accepted standard implemented by (almost) all computers and operating systems all over the world. **ASCII** (which is a short for _American Standard Code for Information Interchange_) is the most widely used system in the world, and it’s safe to assume that nearly all modern devices (like computers, printers, mobile phones, tablets, etc.) use this code.

### Char type declarations

The first way allows us to specify the character itself, but **enclosed in single quotes**: `''` (apostrophes). You’re not allowed to omit apostrophes under any circumstances.

```C
char a = 'A';
```

The second method consists of assigning a **non-negative integer value** that is the ASCII code of the desired character. 

```C
char A = 65;
```

The second solution, however, is less recommended and if you can avoid it, you should. Firstly, because it’s **illegible**. Without knowing ASCII code, it’s impossible to guess what that it really means. Perhaps this is the code for a character, but it can also happen that a sociopathic programmer uses this devious way to save the number of sheep that have already been counted.

The second reason is more exotic, but still true. There’s a significant number of computers in the world which use codes **other than ASCII**. For example, many of the IBM mainframes use a code commonly called **EBCDIC** (_Extended Binary Coded Decimal Interchange Code_) which is very different from ASCII and is based on radically different concept.

### Escaping

The `\` character (called _backslash_) acts as an **escape character**, because by using the `\` we can escape from the normal meaning of the character that follows the slash. In this example, we **escape** from the usual role of the apostrophe (i.e., delimiting the literals of type `char`).

- `\n` – denotes a **transition to a new line** and is sometimes called an **LF** (**Line Feed**), as printers react to this character by pulling out the paper by one line of text.

- `\r` – denotes the **return to the beginning of the line** and is sometimes called a **CR** (**Carriage Return** – “carriage” was the synonym of a “print head” in the typewriter era); printers respond to this character as if they are told to re-start printing from the left margin of the already printed line.

- `\a` (as in **alarm**) is a relic of the past when teletypes were often used to communicate with computers; sending this character to a teletype turns on its ringer; hence, the character is officially called **BEL** (as in **bell**); interestingly, if you try to send the character to the screen, you’ll hear a sound – it won't be a real ringing but rather a short beep. The power of tradition works even in the IT world.

- `\0`  called **nul** (from the Latin word **nullus** – none) is a character that **does not represent any character**; despite first impressions, it could be very useful.

You can also use the escape character to **escape from the escape character** (`\\`).

_Exception_: Specifier character as seen afterwards uses %, to escape it: `%%` (as in _itself_) specifies the **percent sign**.

There is also a variant when a backslash is followed by two or three **octal digits** (the digits from the range of 0 to 7). A number coded in this manner will be treated as an **ASCII value**. It may look like this:

```C
Character = '\47';
```

`047` octal is `39` decimal. Look at the ASCII code table and you'll find that this is the ASCII code of an apostrophe, so this is equivalent to the notation for `'\''`.

The second escape refers to the situation when a `\` is followed by the letter `X` (lower case or upper case – it doesn't matter). In this case there must be either one or two **hexadecimal digits**, which will be treated as ASCII code.

### Char values are int values

The `char` type is treated as a special kind of `int` type. This means that:

- You can always **assign a `char` value** to an `int` variable;
- You can always assign an `int` value to a `char` variable, but if the value exceeds 255 (the top-most character code in ASCII), you must expect a loss of value;
- The value of the `char` type can be subject to the **same operators** as the data of type `int`

The _long_ and _short_ modifiers **must not be used** in conjunction with the type `char`, but we can use the `unsigned` modifier. Most of the compilers currently in use assume that the `char`s are stored using 8 bits (1 byte). That may be enough to store a small value such as the number of months or even the day of the month.

If we treat the `char` variable as a signed integer number, its range would be [-128 .. 127]. If we don’t need any signed value, its range shifts to [0 .. 255]. This may be sufficient for many applications and may also result in significant savings in memory usage.

## Literal

Now’s probably a good time to bring a new term into the mix: a **literal**. The literal is a symbol which **uniquely identifies its value**. Some prefer to use a different definition: the **literal means itself**. Choose the definition that you consider to be clearer and look at the following simple examples:

- `Character` - this is not a literal; it’s probably a variable name; when you look at it, you cannot guess what value is currently assigned to that variable;
- `'A'` - this is a literal; when you look at it you can immediately guess its value; you even know that it’s a literal of the `char` type;
- `100` - this is a literal, too (of the `int` type);
- `100.0` - this is another literal, this time of a floating point type;
- `i + 100` - this is a combination of a variable and a literal joined together with the `+` operator; this structure is called an **expression**.

## Operators and operations

An **operator** is a symbol of the programming language which is able to **operate** on the values.

We’ll begin with the operators associated with widely recognisable **arithmetic operations**. The order of their appearance is not accidental.

### Multiplication and Division (binary operators)

An asterisk (`*`) is a **multiplication** operator.

A slash (`/`) is a **divisional** operator. The value in front of the slash is a **dividend**, the value behind the slash, a **divisor**.

Division by zero is strictly **forbidden**, but the penalty for violating this rule will come to you at different moments. If you dare to write something like that, a judgement will be issued by the compiler – you may get a **compilation error** and you won't be able to run your program or the program may **terminate abnormally** and produce unreliable results.

### Addition and subtraction (binary and unary operators)

The **addition** operator is the `+` (plus) sign, which is one that we already know from mathematics

The **subtraction** operator is obviously the `-` (minus) sign, although you should note that this operator also has another meaning – it can change the sign of a number.

It has been said that addition is not always commutative in C. Imagine that you have to add a large number of floating-point values – some of them are very large, some very small (close to zero). As our computer only saves 8 precise digits of any `float`, adding both could possible result in the lower value simply vanishing without a trace. We can’t avoid these effects when we add/subtract the numbers of type `float` (and of `double` as well, because they’re also affected by this issue). The phenomenon described here is what we call a **numerical anomaly**.

#### Unary minus

In “subtracting” applications, the minus operator expects two arguments: the left (a **minuend** in arithmetic terms) and the right (a **subtrahend**). For this reason, the subtraction operator is considered one of the binary operators, just like the addition, multiplication and division operators. But the minus operator may be used in a different way , to change the polarity of an integer:

```C
int i;
i = -i;
```

A plus in the unary sense its syntactically correct but does nothing (just the same as mathematics)

### Remainder (binary)

The **remainder** operator (or **modulus** as it is often called) is quite a peculiar operator, because it has no equivalent among traditional arithmetic operators. Its graphical representation in the “C” language is the following character: `%` (percent). Both arguments cannot be floats (don't forget this!). You cannot compute the **remainder** with the right argument equal to zero. 

### Prefix and postfix operators (unary)

The `++` (plus plus) operator increments the value by one and the `--` (minus minus) decrements it by one. They can be both at the start of the variable (prefix) or at the end of the variable (postfix). The behaviour changes as: _pre-_ because the variable is modified **first** and then its value is **used**; _post-_ because the variable's value is **used** and then **modified**.

### Shortcut Operators

If `op` is a **two-argument operator** (binary - this is a very important condition!) and the operator is used in the following context:

`variable = variable op expression;`

then this expression can be **simplified** as follows:

`variable op = expression;`.

This includes : `+=`, `-=`, `*=`, `/=`, `%=`, `<<=`, `>>=`, `&=`, `^=`, `|=`

### Logical Operators

`==` is a **binary** operator with left-side binding. It needs two arguments and checks if they’re equal.

In addition, there’s another operator that can be used to construct conditions. It’s a unary operator performing a **logical negation**. Its operation is simple: it turns true into false and false into true. This operator is written as a single character `!` (_exclamation mark_) and its priority is very high: the same as the increment and decrement operators.

You have also both `>` (**greater than**) operator and `<` (**smaller than**) operator in C. Both have another special, non-strict variant, but it’s denoted differently in classical arithmetic notation: `>=` (**greater than or equal**) and `<=` (**smaller than or equal**). There are two subsequent signs, not one. Both of these operators (strict and non-strict) are binary operators with left-side binding.

Answer to logical operators operations are either true which is represented `1` and false which is represented as a `0`.

In the language of logic, the connection of conditions is called a **conjunction** and is represented by the term **and**. While the term **or** means that the result depends on at least one of these conditions. In logic terms, this is called a **disjunction**

The logical conjunction operator in the “C” language is a digraph `&&` (_ampersand ampersand_) and the disjunction operator is the digraph `| |` (_bar bar_)

#### Bitwise operators

>Logical operators take their arguments as a whole, **regardless of how many bits they contain**. The operators are aware only of the value: `0` (when all the bits are reset) means `false`; not `0` (when at least one bit is set) means `true`. The result of their operations is one of the values: `0` or `1`.
>
>However, there are four operators that allow you to manipulate single bits of data. We call them **bitwise operators**. They cover all the operations we mentioned before in the logical context and one additional operator. This is the _xor (exclusive or)_ and is denoted as `^` (caret)

- & (ampersand) -> Bitwise conjunction (AND)
- | (bar) -> Bitwise disjunction (OR)
- ~ (tilde) -> Bitwise negation (NOT)
- ^ (caret) -> Bitwise exclusive disjunction (XOR)

>Arguments of these operators **must be integers** (`int` as well as `long`, `short` or `char`); we must not use `float` here.

> Bitwise operators are stricter: **they deal with every bit separately**. If we assume that the `int` variable occupies 32 bits, you can imagine the bitwise operation as a 32-fold evaluation of the logical operator for each pair of bits of the arguments. Obviously, this analogy is somewhat imperfect, as in the real world all these 32 operations are performed at the same time.

Note -> Keep in mind when flipping binary values of the **two's complement numbers**.

The bitwise operators we have just seen are often used to change values within registers that have a certain number of bits, each indicating a different flag for the processor. In this task you may need to:

- **check the state** of your bit – you want to find out the value of your bit; comparing the whole variable to zero will not do anything, because the remaining bits can have completely unpredictable values, but we can use the following conjunction property.
```C
x & 1 = x
x & 0 = 0
```
   A sequence of zeros and ones whose task is to grab the value or to change the selected bits is called **a bitmask**. To build one, imagine that we want to change the third bit, which has the weight of 2^3 = 8 and therefore `int TheMask = 8`. Depending on how we selected the mask, there are two options

**Reset your bit** - you assign a zero to the bit while all the other bits must remain unchanged; we’ll use the same property of the conjunction as before, but we’ll use a slightly different mask where only the bit we want is 0, finally resulting in a trivial operation:

```C
FlagRegister &= ~TheMask
```

**Set your bit** – you assign a `1` to your bit while all the remaining bits must remain unchanged:
```C
FlagRegister |=The
```

**Negate your bit** – you replace a `1` with a `0` and a `0` with a `1`. We’ll use an interesting property of the _xor_
#### Bit shifting operators

Another operation relating to single bits which is only applied to integer values. In computers, as 2 is the base for binary numbers (not 10), shifting a value one bit to the left corresponds to multiplying it by 2; respectively, shifting one bit to the right is like dividing by 2 (notice that the right-most bit is lost). Bit shifting then, can be:

- **Logical**, if all the bits of the variable are shifted; shifting takes place when you apply it to unsigned integers
- **Arithmetical**, if the shift omits the **sign bit** - in two's complement notation, the role of the **sign bit** is played by the **highest bit** of a variable; if it's equal to "1", the value is treated as negative; this means that the arithmetic shift cannot change the sign of the shifted value.

The shift operators in the “C” language are a pair of digraphs, `<<` and `>>` clearly suggesting in which direction the shift will act. The left argument of these operators is the integer value whose bits are shifted. The right argument determines the size of the shift. This shows that this operation is certainly not commutative

### Size operator
The `sizeof` operator is a **unary** prefix operator and with the highest possible priority.It expects that its argument is a **literal**, or a **variable**, or an **expression** enclosed in parentheses, or the **type name** (this is the only “C” operator which allows its argument to be a type). It provides information on how many bytes of memory its argument occupies (or may occupy). For example:

```C
char tab[10];
i = sizeof tab;
```

In which variable i will be set to the value 10 as char types occupy just one byte (it takes the **entire** `tab` array). Values of the `int` type occupy 32 bits, i.e., 4 bytes in most modern compilers/computers, **but we cannot guarantee** that this is true in all cases.

The `sizeof` is not only an operator – it’s also a **keyword**.
### Priorities

The “C” language precisely defines the **priorities** of all operators and assumes that operators of a larger (higher) priority perform their operations before the operators with a lower priority. This is called ***the hierarchy of priorities***. For  operators as seen here(highest to lowest):

1. `()`, `[]`, `->`, `.`
2. `++` (prefix), `--` (prefix), `+` (unary), `-` (unary), `!`, `~`, `*`(unary), `&` (unary), `sizeof`, `_Alignof`
3. `*`, `/`, `%`
4. `+`, `-`
5. `<<`, `>>`
6. `<`, `<=`, `>`, `>=`
7. `==`, `!=`
8. `&`
9. `^`
10. `|`
11. `&&`
12. `||`
13. `? :` (conditional operator)
14. `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `<<=`, `>>=`, `&=`, `^=`, `|=`
15. `,`
16. `++` (postfix), `--` (postfix)

One should be careful about the different working procedures of the operators:

```C
int j = 4;
i = 2 * j++
```

In this case, i =8 and j = 5
### Bindings

The **binding** of the operator determines the order of the computations performed by some operators with equal priority, put side by side in one expression. Most operators in the “C” language have the **left-sided** binding, which means that the calculation of the expression shown here is conducted from **left to right**. 

Of course, we’re always allowed to use **parentheses**, which can change the natural order of calculation. Just like with arithmetic rules, subexpressions in parentheses are always calculated first. You can use as many parentheses as you need and we often use them to improve the readability of an expression, even if they don't change the order of operations.

Additions performed by computers are not always commutative.

## Input and Output

Sending data in the direction from human (user) to the computer program is called **input**. The stream of data transferred in the opposite direction, i.e. from the computer to the human, is called **output**.

### Output

The `puts` function has already been used in this notes, which allowed the code to output some information to he screen. The `puts` function's capabilities aren't really all that stunning – its argument can only be a **string** (more precisely data of type `char *` – this will be defined in depth in Module 4). You mustn’t use it if you want to print an integer value or a single character. `puts` expects only one argument: the pointer to the string to be printed:

```C
/*
Protype of puts function
@param char* s
*/
int puts(char* s);
```

The `int` returned it’s a non-negative number if everything goes well and `-1` if `puts` cannot meet our demands due to any reason.

There’s a very powerful function in the “C” language named `printf` (**print formatted**). This function can easily output several values of different types and mix them with the text.  `puts` (in contrast to `printf`) **automatically appends a newline character** to the output.

This `printf` function doesn’t specify how many arguments must be provided; the only requirement is that there must be at least one argument; additionally, only the first argument has a strict type (it must be a string); all subsequent arguments may be of any type. The first, mandatory, argument is called the **format** and it’s a recipe or a specification according to which the `printf` function will proceed with its subsequent arguments.

```C
/*
Protype of printf function
@param char* format
*/
int printf(char* format, ...);
```

Where three dots indicate that an arbitrary (including zero) number of parameters may appear in their place.

If there’s a percent symbol inside the format, the `printf` considers it a **hint on how to proceed** with the arguments following the format:

```C
printf("Sheep counted so far: %d", SheepCounter);
```

The `%` joined together with some other character(s) is sometimes called a **specifier**. Some examples are:

- `%d` (as in **d**ecimal) specifies that the corresponding argument is a **value of type `int`** and should be presented as a fixed-point decimal number; its synonym is a `%i` specifier (as in **i**nteger).
  
- `%x` (as in he**x**adecimal) specifies that the corresponding argument is a value of type `int` and should be presented as a fixed-point **hexadecimal number**.
  
- `%o` (as in **o**ctal) specifies that the corresponding argument is a value of type `int` and should be presented as a fixed-point **octal** number.
  
- `%c` (as in **c**har) specifies that the corresponding argument is a value of type `int` or `char` and should be presented as a **character**.
  
- `%f` (as in **f**loat) specifies that the corresponding argument is a value of type `float` and should be presented as a **single-precision floating-point number**.
  
- `%lf` specifies that the corresponding argument is a value of type `double` and should be presented as a **double-precision floating-point number**.

- `%s` (as in **s**tring) specifies that the corresponding argument is a value of type `char*` or `char[]`

he string sent to the screen by the `printf` function will appear **character by character** and if you don't request it explicitly it will **fill the entire line** from the left to right margin of the screen (or the window). To specify a new line, refer to the escape section.

### Input

It’s difficult to imagine any complex program that does not require any data from the user, although sometimes, encoding all the data needed inside the source code (which is sometimes called **hard coding**) is theoretically possible (or may be required), its not an elegant nor particularly convenient solution.

For this task, the function is named `scanf` (**scan formatted**) and is a close relative of the `printf` function. 

```C
scanf("%d", &MaxSheep);
```

The first parameter is also a **format** that tells the function which data will be given to the program, and in which form. As before, we give arguments for the format in the amount equal to the number of the given specifiers. The second parameter can either be a variable or an expression.

You probably have already wondered what is the `&` operator. `scanf` needs something completely different: precisely **where is the variable placed in the memory?** The mysterious `&` is a unary operator which gives the information about its argument's location. The `scanf`'s format provides information about the **type** of the data while the `&`, along with the variable name, says **where** it has to be placed. Leaving out the `&` doesn’t cause any problems during compilation, so therefore you have to remember that `scanf` **essentially needs it** and cannot operate without the `&`.


