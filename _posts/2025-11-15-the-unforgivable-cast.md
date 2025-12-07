---
title: The Unforgivable Cast
date: 2023-11-15 22:32:00 +0530
categories: [C++, Coding ]
tags: [c++, coding]     # TAG names should always be lowercase
comments: true
---

> “Today,” growled Mad-Eye Moody, “we’re going to learn about the unforgivable cast.”
> He scribbles on the board `(T)expr`, the chalk screeching. 
> “Use this,” he snarled, “and you might as well pack your bags for Azkaban.”


Yes, the most harmless looking cast, the C-Style cast, should be an unforgivable cast.
Why unforgivable? Because it is just so damn powerful... It's simple syntax lures you in, the elegance comforts you.... It looks so much cleaner and simpler than `static_cast<T>(exp)`... Ewww so verbose, so inelegant...


The syntax is so minimal that it feels like you're under the Imperius Curse: you have no will, you just do it. 
The bugs will tortur you like the Cruciatus Curse.
And if you ever have to track one down in production, you’ll start wishing for the Killing Curse instead.

Okay, enough scaring you. First let's find out what it actually does. C-Style casts are not simple like static_cast or reinterpret_cast. They are actually multiple types of casts rolled into one.

## 1. const_cast
This alone should send chills down your spine. The very first thing it does is `const_cast`. One wrong move and you are in UB land. Consider the following code:

```cpp
class A;
class C: private A {
}

void foo(A& obj);

int main(){
  const C c = C{};  
  foo(c);           # Fails to compile
  foo((A)c);        # Works
}
```

When `foo(c)` does not work, slapping on a cast makes everything magically compile! So you think you are probably done, the compiler is no longer crying and life is good. 
But foo could be modifying the obj. Which takes you to undefined behaviour land.

The only proper use for const_cast is when you must interact with APIs beyond your control. Legacy APIs or poorly designed but widely used ones, where you know the object won’t be modified but isn’t marked const, and you can’t fix it.

> Modifying a const object is UB, and C-Style cast make it very easy to cast away constness

## 2. static_cast & static_cast + const_cast
Most of the time, you probably want static_cast: converting int to double, upcasting objects, etc.

But even here, it does more than a static_cast. It just ignores the access specifiers. For those who have forgotten, access specifiers are `private, protected and public` defining which context is allowed to access which variable/function.

```cpp
class A {};
class B : private A {};
```

If you try `static_cast<A>(b)` on an object of type B. It will fail. because A is private, and it should not have access to A, in this scope. But... C-Style cast does not care. It is all too powerful. It's magic beyond us mere mortals.

## 3. reinterpret_cast
This is the truly dangerous part. It’s probably not what you intended when you wrote a C-style cast, but the compiler will happily reinterpret memory for you.

Hey, these bits here, you think are A.... No, they are B. Treat them as B, it's alright. And it is very suscptible to introduce subtle bugs. Consider the following case

```cpp
class A{int a;};
class B{int b;};
class C: public A, public B{int c;};

void foo(B& obj);

int main(){
  const C c = C{};  
  foo((B)c);        
}
```
The memory layout of C is such that object of A is located at the address (p), then the object of type B is located at (p+4)

So when converting a C to a B, the compiler must adjust the pointer.

`static_cast<B>(c)` does this correctly.
`reinterpret_cast<B>(c)` does not.... it keeps the original address.

Reinterpret cast, just tells the compiler. This memory right here.. yes, this is B now, just treat it like that.

Anyways, but for this case, our code was still working right... What is the issue? The C-Style cast, tries to perform a static_cast, and it succeeds.

But imagine someone refactors the code and removes inheritance from B. `static_cast<B>(c)` would've thrown a very clear error, that we are doing something illegal.
A C-style cast? Oh no. It will still happily give you a B, whether it makes sense or not.

This I find is the one of the biggest weakness of C++. It is un-necessarily verbose about mundane things, but too casual about things which are too powerful.
The ugliness and code bloat that using static_cast<T>() adds to your code is horrendous. So it is only natural that you reach for the naive looking C-Style cast.

It is just code debt, the legacy or the curse of C, that C++ now has to live with, which C++ fanboys like to call as features, elegance, where the code is subtle, and verbose and terse when using static_casts and others.
There is no consistency, just justifications for self-satisfaction






Thank you![^youtube]

[^youtube]: Inspired from this very interesting youtube vide https://www.youtube.com/watch?v=SmlLdd1Q2V8





