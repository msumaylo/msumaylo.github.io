---
layout: essay
type: essay
title: "Smartly Avoiding Silence and Smartass Responses"
# All dates must be YYYY-MM-DD format!
date: 2022-01-27
labels:
  - Stack Overflow
  - Questions and Answers
---

## Intro

<img class="img-fluid" src="../img/apple-touch-icon_400x400.png">

On the subject of getting an answer, Eric Raymond states in [*How to ask questions the smart way*](http://www.catb.org/esr/faqs/smart-questions.html) that:

<blockquote>
Never assume you are entitled to an answer. You are not; you aren't, after all, paying for the service. You will earn an answer, if you earn it, by asking a substantial, interesting, and thought-provoking question — one that implicitly contributes to the experience of the community rather than merely passively demanding knowledge from others.</blockquote>
  
Asking questions is an integral part to learning and communication. However, in a technical field such as software engineering, asking technical questions the “smart” way ensures that you will receive an answer that will likely be more prevalent to the issue that needs to be resolved. “Smart” questions are much more than just a simple yes or no question, and require effort on part of the asker to be formed.

Prior to creating a “smart” technical question, Raymond notes that hackers and other technical people “like answering questions for people who have demonstrated they can learn from the answers”. To do so, he notes that you should try finding the answer yourself, through the use of other resources such as documentation, FAQs, Google searches of other similar questions, or through your own experimentation. By showing you have done this prior to asking a question, Raymond states that it shows that “you’re not being a lazy sponge and wasting people’s time”. 

Stack Overflow is one such resource, and may be one of, if not the most ubiquitous. The site allows for individuals to submit various programming-related questions, such as how to resolve a bug in one’s code. Other users are able to provide answers, and vote on helpful answers or solutions.

## Example 1: a "smart" question

Let’s see what a “smart” question looks like. [Here](https://stackoverflow.com/questions/295579/fastest-way-to-determine-if-an-integers-square-root-is-an-integer) is a question on determining the fastest way to determine if the square root of an integer is an integer: 
```
Fastest way to determine if an integer's square root is an integer


I'm looking for the fastest way to determine if a long value is a perfect square (i.e. its square root is another integer):

I've done it the easy way, by using the built-in Math.sqrt() function, but I'm wondering if there is a way to do it faster by restricting yourself to integer-only domain.
Maintaining a lookup table is impractical (since there are about 231.5 integers whose square is less than 263).
Here is the very simple and straightforward way I'm doing it now:

public final static boolean isPerfectSquare(long n)
{
  if (n < 0)
    return false;

  long tst = (long)(Math.sqrt(n) + 0.5);
  return tst*tst == n;
}
Note: I'm using this function in many Project Euler problems. So no one else will ever have to maintain this code. And this kind of micro-optimization could actually make a difference, since part of the challenge is to do every algorithm in less than a minute, and this function will need to be called millions of times in some problems.

I've tried the different solutions to the problem:

After exhaustive testing, I found that adding 0.5 to the result of Math.sqrt() is not necessary, at least not on my machine.
The fast inverse square root was faster, but it gave incorrect results for n >= 410881. However, as suggested by BobbyShaftoe, we can use the FISR hack for n < 410881.
Newton's method was a good bit slower than Math.sqrt(). This is probably because Math.sqrt() uses something similar to Newton's Method, but implemented in the hardware so it's much faster than in Java. Also, Newton's Method still required use of doubles.
A modified Newton's method, which used a few tricks so that only integer math was involved, required some hacks to avoid overflow (I want this function to work with all positive 64-bit signed integers), and it was still slower than Math.sqrt().
Binary chop was even slower. This makes sense because the binary chop will on average require 16 passes to find the square root of a 64-bit number.
According to John's tests, using or statements is faster in C++ than using a switch, but in Java and C# there appears to be no difference between or and switch.
I also tried making a lookup table (as a private static array of 64 boolean values). Then instead of either switch or or statement, I would just say if(lookup[(int)(n&0x3F)]) { test } else return false;. To my surprise, this was (just slightly) slower. This is because array bounds are checked in Java.

```
Since the asker wants to know how to do something, they start with describing what their end-goal is, in addition to having said goal explicitly in the title. After that, they then show the method they are currently using, and demonstrate that they have already made use of various other methods to solve their problem. They also provide specific context with the environment the function is for, such as the function being used for Project Euler problems, and that adding 0.5 to Math.sqrt() is not necessary on their machine from their testing.

As a result, the asker received 35 answers, with several being very comprehensive. Here is a snippet of the first answer:

```
794

I figured out a method that works ~35% faster than your 6bits+Carmack+sqrt code, at least with my CPU (x86) and programming language (C/C++). Your results may vary, especially because I don't know how the Java factor will play out.

My approach is threefold:

First, filter out obvious answers. This includes negative numbers and looking at the last 4 bits. (I found looking at the last six didn't help.) I also answer yes for 0. (In reading the code below, note that my input is int64 x.)
if( x < 0 || (x&2) || ((x & 7) == 5) || ((x & 11) == 8) )
    return false;
if( x == 0 )
    return true;
Next, check if it's a square modulo 255 = 3 * 5 * 17. Because that's a product of three distinct primes, only about 1/8 of the residues mod 255 are squares. However, in my experience, calling the modulo operator (%) costs more than the benefit one gets, so I use bit tricks involving 255 = 2^8-1 to compute the residue. (For better or worse, I am not using the trick of reading individual bytes out of a word, only bitwise-and and shifts.)
int64 y = x;
y = (y & 4294967295LL) + (y >> 32); 
y = (y & 65535) + (y >> 16);
y = (y & 255) + ((y >> 8) & 255) + (y >> 16);
// At this point, y is between 0 and 511.  More code can reduce it farther.
To actually check if the residue is a square, I look up the answer in a precomputed table.
...
```
## Example 2: a "not so smart" question

Now, we will take a look at a “not so smart” question. [Here](https://stackoverflow.com/questions/4955198/what-does-dereferencing-a-pointer-mean) is a question about dereferencing a pointer in C/C++:

```
What does "dereferencing" a pointer mean?


Please include an example with the explanation.
```
This question is too simple. This question would likely have been solved just from a quick Google search or with a quick browse through a C/C++ reference site. The asker does not elaborate if they already did a Google search or not, but we can probably assume that they did not. 

This question would receive 6 answers. Fortunately for the asker, the first answer was a very comprehensive explanation of pointer dereferencing. Here is a snippet of the start of said answer: 

```
Reviewing the basic terminology
It's usually good enough - unless you're programming assembly - to envisage a pointer containing a numeric memory address, with 1 referring to the second byte in the process's memory, 2 the third, 3 the fourth and so on....

What happened to 0 and the first byte? Well, we'll get to that later - see null pointers below.
For a more accurate definition of what pointers store, and how memory and addresses relate, see "More about memory addresses, and why you probably don't need to know" at the end of this answer.
When you want to access the data/value in the memory that the pointer points to - the contents of the address with that numerical index - then you dereference the pointer.

Different computer languages have different notations to tell the compiler or interpreter that you're now interested in the pointed-to object's (current) value - I focus below on C and C++.

A pointer scenario
Consider in C, given a pointer such as p below...

const char* p = "abc";
```
Other comments also provide links to other learning resources. One response would just be a [link](https://stackoverflow.com/questions/2795575/how-does-dereferencing-of-a-function-pointer-happen) referring to another Stack Overflow question, albeit a more fleshed out version of the question that was asked.

## Conclusion

In conclusion, the amount of effort one puts into a question can be equivalent to the amount of effort provided in an answer. If you want an answer that you will be able to make use of, you must show that you made significant attempts to figure out the answer but could not reach a solution.


