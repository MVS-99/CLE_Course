## Arrays
So far, we’ve declared variables that can store exactly one given value at a time. These variables are called _scalars_, analogous to mathematical terms. All variables we’ve used so far have actually been scalars.

Arrays, in contrast are **multi-value variables**. For example if we create:

```C
int numbers[5]
```

The variable called `numbers` it’s intended to store five values (note the number enclosed inside brackets) of type `int`; using the appropriate terminology: `numbers` **is an array consisting of five values of type `int`**. Since such an array is called a _vector_ in mathematical terms, we'll also say that this statement declares an `int` vector of a size equal to five. Our vector is a **collection of elements**, but each **element is a scalar**.

All the elements of an array **have the same type**. There are no exceptions to this rule. There are other programming languages which allow the use of arrays with elements of various types, but “C” is not one of them. The “C” language adopted the convention that the elements in an array are numbered **starting from 0**. This means that the item stored at the beginning of the array will have the number 0. Since there are five elements in our array the last one will have the number 4. **Don't forget this**.

To access the element 5 for example we would need to do:

```C
int example = numbers[4]
```

The value inside the brackets, which selects one element of the vector, is called an **index**, while the operation of selecting an element from the array is known as _indexing_. **Any expression could be the index** too - e.g:

```C
int numbers[5], sum = 0, i;

for(i=0;i<5;i++) sum += numbers[i];
```

We could also rearrange the element of the array by swapping the values , e.g:
```C
for(i=0;i=2;i++){
	auxiliary = numbers[i];
	numbers[i] = numbers[4-i];
	numbers[4-i] = auxiliary;
}
```

As you can imagine, if the swapping of values is allowed, we can also sort the array. There are a multitude of sorting algorithms each and every one with its complexity and fit to specific problems depending on data distribution and size. You may look for more information online that the one provided for the course, which is just a very simple algorithm. Just look for C sorting algorithms and you'll have more information. The buble sort example:
```C
#include <stdio.h> 
int main(void) {
        int numbers[5];
        int i, aux;
        int swapped;
        /* ask the user to enter 5 values */
        for(i = 0; i < 5; i++) {
                printf("\nEnter value #%i\n",i + 1);
                scanf("%d",&numbers[i]);
        }
        /* sort them */
        do {
                swapped = 0;
                for(i = 0; i < 4; i++) {
                        if(numbers[i] > numbers[i + 1]) {
                            swapped = 1;
                            aux = numbers[i];
                            numbers[i] = numbers[i + 1];
                            numbers[i + 1] = aux;
                         }
                }
        } while(swapped);
        /* print results */
        printf("\nSorted array: ");
        for(i = 0; i < 5; i++)
                printf("%d ",numbers[i]);
        printf("\n");
        return 0;
}
```

Arrays can be initiated as scalars do:

```C
int vector[5] = {0, 1, 2, 3, 4};
```

If you provide fewer values than the size of an array, the compiler determines that those elements for which you did not specify any value should be **set to `0`**. While if you provide more elements than can be stored in an array you'll get an error.

Also, an array can also be declared without specifying the size of the array but providing an initiator -  the compiler will **assume that the size** of the array is the **same as the length** of the initiator.

## Pointers

**Pointers** are also **values**, but are different from those we’ve operated with so far. Modern computers have large, fast memories. You know that memory size is expressed in units called **bytes**, and you also know that when you declare any variable, for example, in such an obvious and simple way, the variable **occupies a little piece** of the computer memory. So far, all we’ve needed to know is what value is stored in the variable. From now on, we’re also interested in **where** this value is stored.

### Declaration

This trait of the data (to say it more formally, **attribute**) is often called the **address** - information about where this variable is placed. For example, a pointer `p` that points to a memory address where an int is stored is declared as:

```C
int *p;
```

Where **the presence of the asterisk means that `p` is a pointer** and `int` that the data stored in that address is an integer. The “C” language can use **amorphous pointers** too, which can be used to point to **any data** of **any type**.

If you use void as the type for the pointer, then you create valid pointer to some memory, but interpretation of pointed value belongs to you. We have to mention that you can typecast pointers, but it is, in many cases, bad practice. Think twice before do this!

### Assigning a pointer

A pointer is assigned in the same way you can assign any value to any other variable: by using the `=` operator. A more important question is: which values are we allowed to assign to the pointers? Using a **literal is not an option**.

The compiler will, of course, allow you to write something like `p = 148324;` but if you think that you know what’s stored in the computer's memory at the address _148324_, then you are a clairvoyant and computer programming is just a waste of your time. There is one distinctive exception - **assigning a zero to the pointer variable**, which would declare a **null pointer**.

A **null pointer** as its name suggest ( in Latin, _nullus_ – none) doesn’t point to anything.
It's like a signpost with all the writing removed. It still exists, but with no purpose to the traveller. Despite appearances, this pointer can be very useful and sometimes even necessary.

Due to the fact that assigning a value of zero to a pointer variable sometimes causes misunderstandings and mistakes (some may confuse the pointer with a variable of type int), there’s an unwritten agreement that developers will avoid assigning null pointers.

Instead, they should follow this next convention:

```C
p = NULL;
```

The `NULL` symbol is actually equal to **zero**. It looks like a variable but you cannot modify its value. It’s called a **macro**. The same convention also says that _NULL_ should be assigned only to pointers. This is a matter of care and elegance with regard to the programming style. We have one caveat: if you want to use the NULL symbol, you have to **include one of the following header files**: `stdio.h` or `stddef.h`. The _NULL_ symbol is defined there. Another way to say we created a null pointer (or visualize it for that matter) is to say the `p` pointer is **grounded**.

Now, we may assign to the pointer a value which **points to any already existing variable**. To do that, we need the **unary prefix reference operator** `&`. So that:

```C
int i = 1999
int *p = &i
```

`p` points to the memory address where `i` is stored.

Two `*` indicates a pointer to a pointer,



### Dereferencing

Dereferencing is an operation by which the pointer variable (as we’ll see later, it’s not only a variable, but also an expression that yields a pointer) becomes **synonymous** with the value it points to.

Imagine we declared a pointer and assigned values to the variable it points as well as defining the pointer to point to that value.

```C
int ivar = 2, *ptr = &ivar;
```

To get a value pointed to by the pointer we have to use a well-known operator (the asterisk: `*`) but in a completely new way – as a **dereferencer**. This is done by placeing an asterisk in front of a pointer, and therefore you get a value which is stored at the location pointed to by the pointer -> `int ivar_copia = *ptr`.

Therefore, if you write something like `*ptr = 4;` you **won't change the pointer value**. You’ll instead change the value pointed to by the pointer. This is an important difference.

Dereferencing NULL pointers is strictly forbidden and leads to a **runtime error**, which stops your program's execution at once.

### Relation with arrays

**Pointers** and **arrays** are intertwined. If you see the **name of an array** without the indices, then it’s always a synonym of **the pointer pointing to the first element of the array**. So thar if we’ve declared a pointer to `int` and a three-element array of type `int`:

```C
int *Ptr, Arr[3];
Ptr = &Arr[0];
Ptr = Arr;
```

The two assignments that follow the declaration set `Ptr` to the same value. In other words, the following comparison:

```C
Arr == &Arr[0];
```

is always true.
### Arithmetic

The arithmetic of pointers is significantly different from the arithmetic of integers, as it’s relatively reduced and allows the following operations only:

- **adding an integer** value to a pointer, giving a pointer (_ptr + int → ptr_);
- **subtracting an integer** value from a pointer, giving a pointer (_ptr – int → ptr_);
- **subtracting a pointer from a pointer**, giving an integer (_ptr – ptr → int_);
- **comparing the two pointers** for equality or inequality (this gives a value of type `int` of either `true` or `false`) (_ptr == ptr → int; ptr != ptr → int_).

Any other operations are either prohibited or meaningless and only the ones mentioned above may be used.

Suppose we have the case
```C
int *ptr1, *ptr2, array[3], i, comparison;
ptr1 = array;
ptr2 = ptr1;
comparison = (ptr1 == ptr2);
ptr2++;
i = ptr2 - ptr1
```

This means `ptr1` and `ptr2` point both to `array` first element. If we check both with a `==` operator it yields `1`. In the sum, `ptr2` is added `1`, we can interpret this operation as follows:

- it has taken into account what type is pointed to by the pointer – in our example it’s `int`;
- it has determined **how many bytes of memory the type occupies** (the `sizeof` operator is used automatically for that purpose) – in our case it’s `sizeof` (`int`);
- the value we want to add to the pointer is multiplied by the given size;
- the address which is stored in the pointer is **increased** by the resulting product.

In the case of arrays, as the `int`s that conform it are stored consecutive within the memory, adding 1 points to the following member of the array.

Then, if we were to subtract the pointers it would be calculated as:

- taken into account: the type to which the pointers point (`int`); this means that both pointers need to point to the same type; the compiler will check it.
- the addresses stored in the pointers are subtracted.
- the result of the subtraction is divided by the size of the type pointed to by the pointers.

The final result tells us how many variables of a given type (i.e. `int`) fit between the addresses stored in the pointers. In our case, it’s obviously `1`, and this value will be assigned to the `i` variable.

if you use a pointer as `p[-1]` thats the element immediately before the one p is currently pointng at
## Strings

An array of `char` elements is called an `string`. 

However, in strings there is almost always the following dillemas:  

- How would we know in advance how many characters we want to put into an array?
- And when we put it in there, how do we know how many characters are really used? 
- How do we discover where the end of the text which has been assigned to the array is?

We **cannot use the `sizeof`** operator for this purpose. It’ll tell us how many characters are occupied by the entire array, but won’t tell us how many of them we actually use to store the name. This issue is solved in the "C" language in a special way. Every string must end with a special **tag**, something like a flag waving in the wind and announcing: here is the end of the string – all subsequent characters have no meaning.

This role is played by the character with the **ASCII code equal to 0** `'\0'`. This code does not represent any visible characters and doesn't have any meaning for the input / output devices. We call this character an _empty character_ or _nul_ (don't be confused – it has nothing to do with the NULL pointer).

The convention, though easy to use and understand, has one significant flaw: since we must use one character to indicate where the string ends, it means that we need to count with one more byte when defining the string.

To assign values we can try the array nominal way or the special hard coded in c way:

```C
char protagonist[10] = {'B', 'i', 'l', 'b', 'o', '\0'}; // nominal
char protagonist[10] = "Bilbo" // special
```

We could also define our string as `protagonist[]` and let the compiler **count the characters**. Remember, the compiler will add an empty character to the string.
### Relationship with pointers

Whenever a string appears in the program (like the one here: `"ABCDEFGHIJ"` ), the compiler treats it in a very special way and performs the following steps:

- the compiler **counts how many characters** are inside the string (in our example it’s 10);
- the compiler **reserves memory** for the string but gets **one character more** than the string's length (in our example there will be 11 bytes in use for the string);
- the compiler copies the entire string from our source code into the reserved memory and appends an empty character at the end;
- (pay attention – this is the most important step!) the compiler **treats the string as a pointer** to the reserved memory.

Don't forget: a string is **stored** as a sequence of characters followed by the empty character but **behaves** as a pointer of type `char *`.

This also means that assignments such as (**ARE PROHIBITTED**):

```C
char protagonist[];
protagonist = "Gandalf";
```

The compiler sees the following: there’s a **character array** on the left side of the `=` operator; on the opposite side there’s a **string** (we know it's a value of type `char *`). It would seem that everything’s okay since, as we said earlier, the name of the array is interpreted as a pointer to the first element, therefore both arguments of the `=` operator are pointers of the same type. So what's the problem?

In fact, `protagonist` is a pointer of type `char *` but that pointer has been designed to point to only one location in the memory – the one which stores the `protagonist` array, and nothing else. That pointer cannot be changed.

This assignment tries to force the compiler to change the meaning of the pointer. The compiler’s not going to back down on this. **Making these types of assignments is simply not allowed.**

In order to do this, we need to use the function called `strcpy` (it's a conflation of two words: STRing CoPY). By analogy to the `=` operator, the left argument is the one to which the string is to be copied and the right is the one which is being copied.

```C
strcpy(protagonist, "Gandalf");
```

With that said, notice that if:

1. String is defined as `char* name`: The compiler **assigns the pointer** to a newly reserved string to the "name" variable.
2. String is defined as `char[] name`: Whenever you use the "name" variable it will be interpreted as a **pointer** to the first element.

Therefore if one assigns the string as `name = "Manuel"` the compiler will reserve X bytes (6 in this case) for the new string and fill it with the designated string, ending with the empty character, and then store the pointer of the newly created string in the `name` variable. The regular pointer variable (in contrast to the array name) is a valid **l-value**.

Don't forget, in C:
- apostrophes: `char`
- quotes: `char *`

We can even use `strcpy` for this case too, as it has no intention of changing the pointer's value, it only copies the string along with its empty character into the location pointed by the variable. Note, that we have to make sure that the string being copied **is not longer** than the target array - the compiler won't check it. So in the pointer method, while using `strcpy`, make sure that:

- You know for sure **where** the left argument points to.
- There is **sufficient room** to accommodate the string.

### The string.h library

To include you need to include the directive `#include "string.h"`. It includes the functions:

- `strlen` - STRing LENgth – the length of the string. Function used to **count the characters** in a string, excluding the empty character at the end. Counting starts from the beginning of the string. The string given in the parameter is not modified in any way.

```C
char* ptr = "Tomate";
strlen(ptr);
```

- `strcpy` - STRing CoPY - make a copy of the string. It **makes a copy** of a string pointed to by `source` and stores it at the location pointed to by `destination`. The string pointed to by source is not modified in any way. Copying involves all the characters of the string `source`, including the null character at the end. The result of the function is the same pointer as the one specified as `destination`

```C
char string[50];
char* ptr = "Tomate";
strcpy(string, ptr);
```

- `strncpy` - STRing N CoPY - make a n-long copy of the string. It makes a **copy of a maximum _n_ characters** taken from the string pointed to by `source` and stores them in the location pointed to by `destination`. The string pointed to by `source` is not modified in any way. If source contains fewer characters than `n`, all of them are copied. The finishing null character is only added to the copied string if this character is in `n` range. The result is the same pointer that was specified as the destination.

```C
char string[50];
char* ptr = "Tomate";
strncpy(string, ptr, 3);
```

- `strcat` - STRing conCATenation - append a string to another string. It **appends a copy of the string** pointed to by `source` to the end of the string pointed to by `destination`. The null character that originally closes destination is removed. Then a copy of `source` is appended to `destination` along with its closing null character. The string pointed to by source is not modified in any way. The result of the function is a pointer that was specified as the parameter `destination`

```C
char string[50];
char* ptr = "Tomate";
strcat(string, ptr);
```
