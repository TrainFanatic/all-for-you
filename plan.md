# Dev Plan for making all-for-you

[TOC]



## Description

All-for-you is a little program meant to output a personalised polynomial for all your personal polynomial needs!

## Process

Files: From most important to least important

let2num[x] - input letter and output where it is on the alphabet

main[x] - input set of numbers and produces unsimplified personal polynomial

- This may be comprised of even more programs just for tidying up

simplify[x] - input expression and simplifies it (this is optional)

## Input

Simple, input the entire thing as a String



```java
import java.util.Scanner; // import java.util.*
  

```





## Formatting

### General symbols 

$+$ - Addition

$-$ - Subtraction

$*$ - Multiplication

`frac {n} {d}` - Division (inspiration from LaTeX)

[more to be added later]

### Seperating terms

`(25x^2+25x)+150`$\rightarrow$``

look for pairs of these, first: (,). There  is one pair so detect character "("



## Polynomial code

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

## Simplification of terms and expressions

#### Simplification of brackets

There will need to be alot of bracket multiplying in this, so let's start with that:

Let's take, for example, $25(x-2)(x-3)$ which is part of the process of making the Y-O-U polynomial.

$25(x-2)\rightarrow(25\times x)-(25\times-2)\rightarrow25x-50$



That's multiplying a single term with a bracket, but what about quadratics?

$(25x-50)(x-3)\rightarrow$ 

$25x\times x+25x\times-3+-50\times x+-50\times-3\rightarrow$

 $25x^2+75x-50x+150\rightarrow$

 $25x^2+25x+150$

#### Simplification of fractions

Example: $\frac{25x^2+25x+150}{5}$





## Detection of individual parts (terms?)

### Seperating terms

Example: $25x^2+25x-150$

Formatted as `25x^2+25x-150`

`25+75+50`



Check for one of these characters: + - * /  and any instances of `x` (^ is not counted as it is not a term separator). Count how many of them there are and store it as variable `n`

```java
//Scanner and reading have been routed to variable 'input'
//n is how many characters + - * / there are
pattern="[^xX+\-*/]"; //generates pattern excluding operations (except ^) and x 
String alt = input; //alt for String input
int n = alt.replaceAll(pattern, "").length(); //removes all numbers and operation ^ and find length
// n = alt.length();
int expression1 [][] = new int [2n+1][4]; // n being how many 'seperator characters' there are. n+1 is how many terms there are. 
int lengthOfInput=input.length();
```



Let's call putting the String into an array 'harvesting'

Starting from the first character, look until there is a non-number, non-exponent character

```java
int startOfElement = 0; //character position start for element
for (i=0;i<=input.length();i++){
  //expression1[0][]
	if (input.charAt(i).matches("x+\-*/()") == true){
    startOfElement = i;
  }
}
```



Ideal Output:

| Array `expression1[][]` | `[?][0]` | `[?][1]` | `[?][2]` | `[?][3]` |
| ----------------------- | -------- | -------- | -------- | -------- |
| `[0][?]` -1st term      | +25      | x        | ^        | 2        |
| `[2][?]` - 2nd term     | +25      | x        |          |          |
| `[4][?]` - 3rd term     | -150     |          |          |          |

There are still some flaws with this, so create new `expressionnew[][]`

```java
int expressionnew[][] = new int [n][4]
```

`parent.indexOf(String)` is a helpful tool in java that returns a non (-1) answer if String is not found in the output of `parent`

### Expressions with brackets

#### Non-quadratic expressions

Look for the first character, it's a number, so read until the opening bracket

`25(`

Now, take that as a string and take out the last character so that only the number is there.

`25`

Take the length of the string which is 2

Now get the entire string, `25(x-2) `

but cut off the first two characters so that only `(x-2)` is left

There you have it, the two parts. `25` and `(x-2)`



#### Quadratic expressions

Look at the first character, `(`, it's a bracket so read until a closing bracket

`(25x-50)`

Check next character, if it is a number, then something has gone wrong, if it is a bracket. then read till the next bracket

`(x-3)`

Voila, you've successfully dissected the expression!

## Outdated ideas

### Post-harvest array edit

//So, we check every single array value to see if it has $x$ in it that **IS NOT** its own term

```java
for (int i=0;i<=n;i++){ //using i<=n because if array starts from 0, then last term will be n
  for (int j=0;j<=3;j++){ //3 is maximum width of array, as there is no term comprised of more than 4 elements
    if (expression1[i][j]=="x"){
      //since all independent instances of x will always be on [?][0], exclude independent x's
      if (j != 0){
        
      }
   	 }
  	} 
	}
```



| Array `expression1[][]`  | `[?][0]` | `[?][1]` | `[?][2]` | `[?][3]` |
| ------------------------ | -------- | -------- | -------- | -------- |
| `[0][?]` -1st term       | 25       | x        | ^        | 2        |
| `[1][?]` - 1/2 separator | +        |          |          |          |
| `[2][?]` - 2nd term      | 25       | x        |          |          |
| `[3][?]` - 2/3 seperator | -        |          |          |          |
| `[4][?]` - 3rd term      | 150      |          |          |          |

### 