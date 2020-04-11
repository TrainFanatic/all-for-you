# Dev Plan for making all-for-you

### Description

All-for-you is a little program meant to output a personalised polynomial for all your personal polynomial needs!

### Process

Files: From most important to least important

let2num[x] - input letter and output where it is on the alphabet

main[x] - input set of numbers and produces unsimplified personal polynomial

- This may be comprised of even more programs just for tidying up

simplify[x] - input expression and simplifies it (this is optional)

### Polynomial code

lets say you want a personal polynomail for Y-O-U

Y is the 25th letter of the alphabet

O is the 15th

U is the 21st



It becomes, for f(x)

$\frac{25(x-2)(x-3)}{2}+\frac{15(x-1)(x-3)}{-1}+\frac{21(x-1)(x-2)}{2}$

To get to this:

Since y is the 25th letter of the alphabet, and there are 3 letters in the personalised polynomial, you:

Do $25(x-2)(x-3)$ so that for f(2) and f(3), the answer is zero. Dont forget to substitute x=1 and make it so that $25(x-2)(x-3)=25$ therefore $\frac{(1-2)(1-3)}{n}=1$  and in this case, $n=2$

Do the same for O:

$15(x-1)(x-3)$ to make f(1) and f(3) equal to zero

$15(2-1)(2-3)=15\rightarrow\frac{(2-1)(2-3)}{n}=1$

solve for n, $(2-1)(2-3)=-1$, so to get it to equal to 1, divide by -1 to get $\frac{15(x-1)(x-3)}{-1}$

Do same for U ($\frac{21(x-1)(x-2)}{2}$) and add them all together to get $\frac{25(x-2)(x-3)}{2}+\frac{15(x-1)(x-3)}{-1}+\frac{21(x-1)(x-2)}{2}$

### Simplification

There will need to be alot of bracket multiplying in this, so let's start with that:

Let's take, for example, $25(x-2)(x-3)$ which is part of the process of making the Y-O-U polynomial.

$25(x-2)\rightarrow(25\times x)-(25\times-2)\rightarrow25x-50$



How to detect the individual parts, though?

Look for the first character, it's a number, so read until the opening bracket

`25(`

Now, take that as a string and take out the last character so that only the number is there.

`25`

Take the length of the string which is 2

Now get the entire string, `25(x-2) `

but cut off the first two characters so that only `(x-2)` is left

There you have it, the two parts. `25` and `(x-2)`

**ok, but how about actually multiplying them?**



That's multiplying a single term with a bracket, but what about quadratics?

$(25x-50)(x-3)\rightarrow$ 

$25x\times x+25x\times-3+-50\times x+-50\times-3\rightarrow$

 $25x^2+75x-50x+150\rightarrow$

 $25x^2+25x+150$

Whew, that was long.

But, how to dissect it?



Look at the first character, `(`, it's a bracket so read until a closing bracket

`(25x-50)`

Check next character, if it is a number, then something has gone wrong, if it is a bracket. then read till the next bracket

`(x-3)`

Voila, you've successfully dissected the expression!