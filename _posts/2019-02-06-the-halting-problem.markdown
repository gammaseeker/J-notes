---
layout: post
title: The Halting Problem
date: 2019-02-06 18:07:00 -0500
categories: Theory
---
Theoretical computer science has always been a fascinating branch of computer science because it is the field that challenges one's mathematical maturity and critical thinking skills. You feel like a bonafide genius everytime you complete a proof. I am currently taking a class on the theory of computation and one neat problem we discussed is: <strong>The Halting Problem</strong> 
<br>
"Consider a function called `halt(A, I)` which takes in a program `A`, and an input into the program, `I`. `halt(A, I)` will return `true` if the program halts, else it will return `false` if the program goes into an infinite loop. Given a computer program and some input to that program, will the program go into an infinite loop when fed that input?"
```
bool halt(A, I){
    if(A(I) halts){
        return true;
    }else{
        return false;
    }
}
```
Now let's begin thinking about clever inputs into this code. What would happen if we input the program into itself? A program, in its most literal sense, is a sequence of characters and strings. An input, is also a sequence of characters and strings. Let's write a function that will let us pass in just a program which will act as both `A` and `I`
```
bool halt_on_self(A){
    return halt(A, A);
}
```

Everything looks pretty normal so far, but we can actually do something really spooky with the two functions we have created.
