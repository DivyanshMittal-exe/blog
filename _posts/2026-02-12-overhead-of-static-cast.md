---
title: The Overhead of static cast
date: 2026-02-12 23:18:00 +0530
categories: [C++, Coding ]
tags: [c++, coding]     # TAG names should always be lowercase
comments: true
---


[Last time](https://divyanshmittal-exe.github.io/blog/posts/the-unforgivable-cast/) we saw that, to cast between two types, we should not use the C-Style cast

Instead c++ provides us with `static_cast`, `dynamic_cast` and many more to achieve what we want to do correctly.

You will commonly here, people telling you that dynamic_cast has a runtime overhead, whereas a static_cast, does not.

But this is not the truth. While the overhead of static_cast is much less than that of a dynamic_cast. A static_cast also carries some overhead. It has to do a `nullptr` check at runtime!

But why do we need to make a `nullptr` check? Let us look at an example

```cpp
class A{int a;};
class B{int b;};
class C: public A, public B{int c;};

void foo(B& obj);

int main(){
  C c = C{};  
  C* cptr = rand() ? &c : nullptr;
  B* bptr = static_cast<B*>(cptr);
}
```
The memory layout of C is such that object of A is located at the address (p), then the object of type B is located at (p+4)

So when converting a C to a B, the compiler must adjust the pointer.
But what if we pass nullptr to it? 
If we do not check for cptr to be `nullptr` inside the static_cast, we would have wrongly return `nullptr + 4`, which is completely wrong.

We can also verify the same with our handy [compiler explorer](https://godbolt.org/z/xcbfdc99h) 

The assembly is as follows:

```
.L3:
        cmp     QWORD PTR [rbp-8], 0      ; Check cptr for nullptr
        je      .L4                       ; If nullptr, jump to .L4

        mov     rax, QWORD PTR [rbp-8]    ; rax = cptr
        add     rax, 4                    ; rax = cptr + 4 (adjust to B)
        mov     QWORD PTR [rbp-16], rax   ; bptr = adjusted pointer
        jmp     .L5                       ; Skip 

.L4:
        mov     QWORD PTR [rbp-16], 0     ; just set bptr it to nullptr

.L5:
```

The useful work is done in the lines 

```
        mov     rax, QWORD PTR [rbp-8]    ; rax = cptr
        add     rax, 4                    ; rax = cptr + 4 (adjust to B)
        mov     QWORD PTR [rbp-16], rax   ; bptr = adjusted pointer
```

And rest all is the unnecessary overhead because of nullptr.


Thank you!






