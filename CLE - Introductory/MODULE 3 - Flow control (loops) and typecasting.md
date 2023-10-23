## Controlling the flow

Once logical operators and types are defined, there must have a mechanism which allows us to do something if a condition is met and not to do it if it isn’t. To make these decisions, the “C” language has a special instruction. Due to its nature and its application, it’s called a **conditional instruction** (or **conditional statement**).

```pseudo
if(true_or_not) do_this_if_true;
```

This conditional statement consists of the following, strictly necessary, elements in this and this order only:

- **if** keyword;
- left (opening) parenthesis;
- an **expression** (a **question** or an **answer**) whose value will be interpreted solely in terms of “true” (when its value is non-zero) and “false” (when it is equal to zero);
- right (closing) parenthesis;
- an **instruction** (only **one**, but we’ll learn how to deal with that limitation).

How does this statement _work_?

- if the `true_or_not` expression enclosed inside the parentheses represents the truth (i.e. its _value is not equal to zero_), the statement behind this condition (`do_this_if_true`) will be executed;
- if the `true_or_not` expression represents a **falsehood** (its _value is equal to zero_), the statement behind this condition is **omitted** and the next executed instruction will be the one that lies after the conditional statement.

We’ve said that there may be only one statement after the `if` statement. When we have to **conditionally** execute more than one instruction, we need to use braces `{` and `}` which create a structure known as a **compound statement** or (much simpler) a **block**. The block is treated as a single instruction by the compiler.

```C
if(SheepCounter >= 120){MakeABed(); TakeAShower(); SleepAndDream(); } FeedTheSheepdogs();
```

Writing blocks one after the other is, of course, syntactically correct, but very **inelegant**. It may cause the text of our program to run outside the right margin of the editor. There are a few styles of coding the blocks. I, as an engineer working on kernels and low level code, like to use the **Linux kernel variant**:

The kernel style uses [tab stops](https://en.wikipedia.org/wiki/Tab_stop "Tab stop") (with the tab stops set every 8 characters) for indentation. Opening curly braces of a function go to the start of the line following the function header. Any other opening curly braces go on the same line as the corresponding statement, separated by a space. Labels in a `switch` statement are aligned with the enclosing block (there is only one level of indents). Line length used to be limited to 80 characters – it was raised to 100 in 2020, but the original limit is still preferred. A single-statement body of a compound statement (such as if, while, and do-while) need not be surrounded by curly braces. If, however, one or more of the substatements in an `if-else` statement require braces, then both substatements should be wrapped inside curly braces

```C
int power(int x, int y)
{
        int result;

        if (y < 0) {
                result = 0;
        } else {
                result = 1;
                while (y-- > 0)
                        result *= x;
        }
        return result;
}
```

But, what if we want to express alternative routes to conditional clauses? Luckily, the “C” language allows us to express alternative plans. We do this with a second, slightly more complex form of the conditional statement – here it is:

**if** (true_or_false_condition)  
    perform_if_condition_true;  
**else**  
    perform_if_condition_false;

Thus, we have a new word: `else` – this is a keyword (_reserved word_). A statement which begins with `else` tells us **what to do if the condition specified for the `if` is not met**.

So the _if-else_ execution goes as follows:

- if the condition is “`true`” (its value is not equal to zero) the `perform_if_condition_true` is executed and the conditional statement comes to an end;
- if the condition is “`false`” (its value is equal to zero) the `perform_if_condition_false` is executed and the conditional statement comes to an end

Within this syntax, both `if` and `else` may contain **only one statement**. If you’re going to write more than one instruction, you have to use a block `{}`.

Furthermore, if more clauses should be added to the conditional block, C provides `else if`, which behaves like a conditional condition for the if statement.
## Typecasting - Metamorphosis or conversion of data

Changing the type of the data (perhaps combined with a change of its value, which may be caused by a loss of accuracy) is called a **conversion**.

The “C” language knows two types of conversions:

- **implicit conversions**, which work according to language rules and are not specified in the code in any visible way; their operation is silent and automatic;
- **explicit conversions** carried out at the developer's request; the developer should insert them explicitly inside the code indicating which value should be converted and into which resulting type.

Implicit conversions are performed at run-time according to these strict rules. The rules are applied in the order below until all the data used in the particular expression has **the same type** – this condition is very important!

- data of type `char` or `short int` will be converted to type `int` (this is called an **integer promotion**);
- if there is any value of type `float` in the expression, the other data will be converted to `float`;
- if there’s any value of type `double` in the expression, the other data will be converted to `double`;
- if there’s any value of type `long int` in the expression, the other data will be converted to `long int`.

If the context in which the expression is calculated requires another type than the one resulting from the implicit conversions, the last conversion is done to the type requested by the context.

Explicit conversions are introduced into the code using the **typecast** operator. This is a unary operator with a high priority, equal to unary minus priority. You can see it here:

`(type)value`

where `type` is a name or description of the type which the `value` will be converted into.

## Loops
### While

In general, the loop manifests itself as follows:

```pseudo
while (conditional_expression) {
    statement_1;
    statement_2;
    :
    :
    statement_n;
}
```

If you’ve noticed some similarities to the `if` instruction, good job. In fact, there’s only one syntactic difference: we use the word _while_ instead of _if_.

The semantic difference, however, is more important:
- It checks the condition **before** entering the body
- `while` **repeats the execution** as long as the condition evaluates to `true`
- if you want `while` to execute **more than one** statement, you must (like with the `if` statement) use a block – take a look at the code in the editor;
- an instruction or instructions executed inside the loop are called the **loop's body**;
- if the condition is `false` (equal to zero) as early as when it’s tested for the first time, the **body is not executed** even once (note the analogy of not having to wash your hands if they’re not dirty);
- the body should be able to change the condition value, because if the condition is true at the beginning, the body might **run continuously to infinity** (notice that washing changes the state of impurity).

### Do While

There’s another loop in the “C” language which acts as a mirror image of the `while` loop. We say so because in that loop:

- the condition is **checked at the end** of body execution;
- the loop's body is executed **at least once**, even if the condition is not met.

```pseudo
do{  
    statement_1;  
    statement_2;  
    :  
    :  
    statement_n;  
} while(condition);
```

### FOR loop

The last kind of loop available in the C language comes from the observation that sometimes it’s more important to count the **turns of a loop** (iterations) than to check the conditions. It has three essential elements:

- The **initialisation** of the counter (e.g. `i=0`).
- **Checking** the condition (logical operation such as  `i<100`).
- **Updating** the counter (e.g. `i++`)

```C
for(i = 0; i < 100; i++ ){
	/* the body goes here */ 
}
```

The variable used for counting the loop’s turns is often called a **control variable**.

>CAREFUL! The `for` loop has an interesting **singularity**. If we **omit any** of its three components, it’s **presumed that there is a `1` there instead**:

```C
	for( ; ; ) {
	/* the body goes here */ 
}
```

>One of the consequences of this is that a loop written in this way is **an infinite loop**, as the conditional expression is not there, so it’s automatically assumed to be _true_. And because the condition never becomes _false_, the loop becomes infinite.

### Loop candies

So far, we’ve treated the body of the loop as an **indivisible** and **inseparable** sequence of instructions that are performed completely at every turn of the loop. However, the developer could be faced with the following choices:

- it appears that it’s **unnecessary to continue** the loop as a whole; we should refrain from executing the loop’s body and go further;
- it appears that we need to **start the condition testing** without completing the execution of the current turn.

The “C” language provides two special instructions for implementing both of these tasks. Let's say, for the sake of accuracy, that their existence in the language is not necessary – an experienced programmer can code any algorithm without such instructions. The famous Dutch computer scientist **Edsger Dijkstra** proved it in 1965. Additions which don’t improve the language’s power of expression, but only simplify the developer’s work, are sometimes called **syntactic candies**.

These two instructions are:

- `break` - **exits the loop immediately** and unconditionally ends the loop’s operation; the program begins to execute the nearest instruction after the loop's body;
- `continue` – behaves as if the program has suddenly reached the end of the body; **the end of the loop’s body is reached**, the control variable is modified (in the case of for loops), and the condition expression is tested.
## Case and Switch
As you may recall, an _if-cascade_ is the name for a construction of code where **many `if` instructions are placed consecutively one after the other**. There are no obstacles to using and maintaining code like that, but there are a few **disadvantages** that you might not want to have to deal with.

For one, the longer the cascade, the harder it is to read and understand what it’s indented for. Amending the cascade is also hard: it's hard to add a new branch to it and it's hard to remove any previously created branch.

The **case and switch** offers a way to make selections easier. Let me emphasise that this is really more syntax candy that anything else.

### Definition
```C
switch(i) {
        case 1: puts("Only one?"); break;
        case 2: puts("I want more."); break;
        case 3: puts("Not bad."); break;
        case 4: puts("Okay.");
        default: puts("Too much or impossible")
}
```
First, the value of the expression enclosed inside the parenthesis after the `switch` keyword is **evaluated** (this is sometimes called a _switching expression_). Then the block is searched in order to **find a literal** preceded by the `case` keyword which is equal to the value of the expression.

When this case is found, the instructions behind the colon are **executed**. If there’s a `break` among them, the execution of the `switch` statement is terminated, otherwise, all instructions are executed until the end of the block is reached or another `break` is met.

If the switching expression has a value that does not occur in any of the cases, and the `default` keyword is not present, nothing will happen – none of the branches of the `switch` statement are executed.

A few more important remarks to note:
- The value after the case **must not be an expression** containing variables or any other entities whose values aren't known at compilation time;
- The case branches are **scanned in the same order** in which they are specified in the program; this means that the most common selections should be placed first (in fact, this could make your program a little faster in some cases)