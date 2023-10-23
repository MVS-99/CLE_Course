# 1 - On Natural and Programming Languages

A programming language is defined by a set of certain rigid rules, much more inflexible than any natural language.

These rules determine which symbols (letters, digits, punctuation marks, and so on) could be used in the language. This part of the definition of the language is called **lexicon**.

Another set of rules determines the appropriate ways of collating the symbols – this is the **syntax** of the language.

We would also like to be able to recognise the meaning of every statement expressed in the given language – and this is what we call **semantics**.

Any program we write must be correct in these three ways: lexically, syntactically and semantically, otherwise it will neither run nor produce any acceptable results.

A computer is devoid of even a trace of intelligence - it responds only to a predetermined **set of known commands**. A complete set of well-known commands is called an **instruction list (IL)**. The IL is in fact the alphabet of a language, commonly known as a **machine language**, the simplest and most primary language we can use to give commands to the computer.

## Raison d'être of programming languages

It is possible, and often used in practice, for a computer program to be coded directly in machine language using elementary instructions (orders). This kind of programming is tedious, time consuming and highly prone to a programmer's mistakes. At the early stages of computer technology, it was the only available method of programming and it very quickly revealed some serious flaws. Firstly, programming in machine language requires an exhaustive knowledge of the computer’s hardware design and its internal structure. This also means that replacing the computer with one that differs in design can make the programmer's entire knowledge unusable. Also, the old programs could become completely useless if the new computer “used” a different IL. Thus, a program written for a specific type of computer could be completely useless for other computers and vice versa. Secondly, programs written in machine language are very difficult for humans to understand, including experienced programmers. It also takes a long time to develop programs in machine language, and it’s very costly and cumbersome.

All these circumstances led to a need for some kind of **bridge** between the human language (natural language) and the computer language (machine language). That bridge is also a language – an intermediate common language for humans and computers to work together. Such languages are often called **high-level programming languages**.

A high-level programming language is at least somewhat similar to a natural language; it uses symbols, words and conventions readable to humans. This language enables humans to express complex commands for computers and then its translated to IL.

## Compilation

The translation we are referring to is made by a specialized computer program called a **compiler**. The process of translating from a high-level language into a machine language is called **compilation**.

A program (which in fact is just text) is called the source code, or simply source, while the file which contains the source is called the **source file**. The extension will indicate which language is it written on. The sort of structured and semi-formal description of each step of the program is called an **algorithm**.

Next, your source code needs to be **compiled**. To do this you run a compiler, instructing it where you stored the source code that you want to be translated into machine language. The compiler reads your code, does some complex analysis and its first goal is to determine whether or not you made any errors during the coding

If the compiler doesn’t notice any mistakes in your source, the result of its work will be a file containing your program translated into machine language. That file is commonly called an **executable file**. The name of the file depends on the compiler you use and the operating system you’re working with (UNIX ".out" vs WINDOWS ".exe").

Your source code might be comprehensive and divided among several or even dozens of source files. It may also happen that the program was not written by you alone, but by a team, in which case the division of sources into multiple files is simply a must. In such cases, the compiling splits into two phases – a **compilation** of your source, in order to translate it into machine language, and a joining (or gluing) of your executable code with the executable code derived from other developers into a single and unified product. The phase of “gluing” the different executable codes is commonly known as **linking** while the program which conducts the process is called a **linker**.

# Sample program
```C
#include <stdio.h>

int main(void)
{
	puts("It's me, your first program.");
    return 0;
}
```
The character `#` (hash) at the beginning of the first line means that the content of this line is a **preprocessor directive**, a separate part of the compiler whose task is to pre-read the text of the program and make some modifications to it. The prefix “pre” suggests that these operations are performed **before** the full processing (compilation) takes place.

The changes the **preprocessor** introduces are controlled entirely by its **directives**. In the example program, we’re dealing with the include directive. When the preprocessor encounters that directive, it replaces the directive with the content of the file whose name is listed in the directive (in our case, this is the file `stdio.h`). Note – the changes made by the preprocessor never modify the content of your source file in any way. Any alterations are made on a volatile copy of your program, which disappears immediately after the compiler finishes its work.

Writing a program is similar to constructing a building with ready-made blocks. In our program, we’re going to use such a block and we’ll use it when we want to write something on the screen. That block is called puts (you can find it inside our code), but the compiler knows nothing about it so far. In particular, the compiler has no idea that puts is a valid name for that block while puts isn't. The compiler needs to be aware of this. This preliminary information needed by the compiler is included in the files whose names usually end with “_.h_” (**header**). These files are commonly called **header files**.

The **stdio.h** file (defined by the standard of the “C” language) contains a collection of preliminary information about ready-made blocks which can be used by a program to write text on the screen or to read letters from the keyboard. 

One of the most common types of blocks used to build “C” programs is **functions**. If you understand functions only in a purely mathematical sense, this still is a pretty good clue. Imagine a function as a **black box**, where you can insert something into it (not always necessary) and take something new out of it as if out of a magic hat. Things that are put in the box are called function **arguments** (or function **parameters**). Things that are taken out of the box are called function **results**. In addition, a function can do something else on the side. If this sounds rather vague, don't worry, we’ll be talking about functions many times in more detail.

The standard of the “C” language assumes that, among the many different blocks which may be put into a program, one specific block must always be present, otherwise the program won't be correct. This block is always a function of the same name: `main`.

Every function in “C” begins with the following set of information:

- what is the **result** of the function? (`int` - integer)
- what is the **name** of the function? (`main`)
- how many **parameters** does the function have and what are their **names**? (`void` - empty, without content)

in that order. This is sometimes called a **prototype**, and it’s like a label affixed to a function, announcing how we can use that function in your program. The prototype says nothing about what the function is intended for. It’s written inside the function and the interior of the function is called the function **body**. The function body begins where the first opening bracket `{` is placed and ends where the corresponding closing bracket `}` is placed.

We look inside and find a reference to a block called **puts**. This is what we call a **function invocation**. Now let’s consider a few important details.

Firstly, note the **semicolon** at the end of the line. Each instruction (precisely: each statement) in “C” **must end with a semicolon** – without it the program will be incorrect. A statement like this says: instruct the function named puts to show text on the screen. You might ask – how do we know that the puts function will do that for us? Well, we know it from the “C” language standards, but also, the name of the function is an abbreviation of “_PUT String_”. The text intended to be shown on the screen is passed to the function as a function parameter. Remember that the name of the invoked function must always be followed by a pair of parentheses `(` and `)`, even when the function doesn’t expect any parameters from us.

Secondly, the parameter of the function puts is text (string). 

Finally, it is observed at the end:

```C
return 0;
```

this is another **statement** of the “C” language. Its name is just _return_ and that’s exactly what it does. Used in the function, it **causes the end of the function execution**. If you perform `return` somewhere inside a function, this function immediately interrupts its execution. The zero that you see after the word return is the result of your function `main`. This is important – this is how your program tells the operating system the following message: _I did what I had to do, nothing stopped me and everything is OK._ 

The “C” language doesn't force you to use the function results. If the value returned by the function is really needed, we can **make use of it**. But if we **ignore the result**, the compiler will not recognise this as an error. The value returned by the function will simply be rejected. It's not an error.

# On variables

There are special “**containers**” for the purpose of storing the results of these operations in order to use them in other operations. These containers are called **variables**. The name suggests that the contents of a container can be varied in (almost) any way. A variable shall have a **type** a **name** and a **value**.

The variable comes into existence as a result of a **declaration**. A declaration is a syntactic structure that binds a name, provided by the programmer, to a specific type offered by the “C” language. The construction of the declaration (in other words – the declaration syntax) is simple: just use the name of the desired type, then the variable name (or variable names separated by commas if there are more than one). Finally, the value is assigned using the **assignment operator** `=`. The whole statement ends with a semicolon.
## Names

 If you want to give a name to a variable you must follow some strict rules:

- the name of the variable must be composed of **upper-case or lower-case Latin letters, digits and the character** _ (_underscore_);
- the name of the variable must **begin with a letter**;
- the **underline character is a letter** (strange but true);
- upper- and lower-case letters are treated as **different** (case sensitivity)

Note that the same restrictions apply to **function names**.

## Types and values

The _type_ is an **attribute** that uniquely defines which values can be stored inside the variable.  The value of a variable is what we have put into it. Of course, you can only put in a value that is compatible with the variable's type.

Its possible to **declare the variable and assigning the value at the same time**.


# Keywords

(more precisely) **reserved keywords**.

They’re reserved because you mustn't use them as names: neither for your variables, nor functions, nor any other named entities you want to create. The meaning of the reserved word is predefined and mustn’t be changed in any way. Fortunately, because the “C” compiler is **case-sensitive**, you can modify any of these words by changing the case of any letter, thus creating a new word, which is not reserved any more.
## Standard Keywords

- `auto`
- `break`
- `case`
- `char`
- `const`
- `continue`
- `default`
- `do`
- `double`
- `else`
- `enum`
- `extern`
- `float`
- `for`
- `goto`
- `if`
- `inline`
- `int`
- `long`
- `register`
- `restrict`
- `return`
- `short`
- `signed`
- `sizeof`
- `static`
- `struct`
- `switch`
- `typedef`
- `union`
- `unsigned`
- `void`
- `volatile`
- `while`
- `_Alignas`
- `_Alignof`
- `_Atomic`
- `_Bool`
- `_Complex`
- `_Generic`
- `_Imaginary`
- `_Noreturn`
- `_Static_assert`
- `_Thread_local`

## Conditional Compilation Keywords (Preprocessor)

- `#define`
- `#elif`
- `#else`
- `#endif`
- `#error`
- `#if`
- `#ifdef`
- `#ifndef`
- `#include`
- `#line`
- `#pragma`
- `#undef`



# Comments

The developer may want to put in a few words addressed not to the compiler but to humans, usually to **explain** to other readers of the code how the tricks used in the code work, or the meanings of variables and functions and eventually, in order to keep stored information on who the author is and when the program was written.

Good (and responsible) developers describe each function; in particular, they explain the role of the parameters, the value the function returns as a result and what the function actually does.

How do we leave this trace in the source code? It has to be done in a way that won't force the compiler to interpret it as part of the code. A remark inserted into a program which is omitted at the time of compiling is called a _comment_.

If we want to be precise, we should say that each comment is lexically equivalent to **one space**. Whenever the compiler encounters a comment in your program, the comment is completely transparent to it – from the compiler’s point of view, this is only one space (regardless of how long the real comment is).

In the “C” language a comment is a text that begins with the pair of characters:

`/*`

and ends with the pair of characters:

`*/`

The comment can span several lines or it can occupy only one line or only part of a line.

Comments may be **useful** in another aspect – you can use them to mark a piece of code that currently isn't needed for whatever reason. We often do this during the testing of a program in order to isolate the place where an error might be hidden.

Do not **nest comments** as it is prone to errors (`/*8/*a*/*/`)