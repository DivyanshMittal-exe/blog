---
title: Doing more makes you faster
date: 2023-11-01 22:15:00 +0530
categories: [C++, Coding, Optimisation]
tags: [c++, coding, optimisation]     # TAG names should always be lowercase
comments: true
---


Less code means faster code... right?

Take these two pieces of code for example



<figure style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 10px;
  justify-items: center;
">
  <img src="/assets/images/more_work_makes_you_faster/code_with_memset.png" alt="Code with memset" style="width: 100%; max-width: 400px; height: auto;">
  <img src="/assets/images/more_work_makes_you_faster/code_without_memset.png" alt="Code without memset" style="width: 100%; max-width: 400px; height: auto;">
</figure>


Hmmm, clearly the first one is doing more work. Surely, `memset`-ing to 0 will make us slower, right?
Well, only one way to find out. Let’s test it.


![ Benchmark ](/assets/images/more_work_makes_you_faster/Performance_graph.png)


Doing a `memset` before assigning to the struct,[ makes us 3 times faster! ](https://quick-bench.com/q/HVvZsxOLyZInBjrK8AxcRxyobk4){:target="_blank"}


But why is that so? We need to look under-the-hood. What exactly is the assembly doing ?


The normal version compiles to this: 3 instructions to write 7B of data
```assembly
movl $0x2a, 0x8(%rsp)    ; p.id = 42
movb $0x41, 0xc(%rsp)    ; p.flag = 'A'
movw $0x200, 0xe(%rsp)   ; p.code = 512
```

But with our memset optimisation, we get this. The whole struct (8 bytes) is written in one go.
```assembly
movabs $0x20000410000002a,%rax
mov    %rax, 0x8(%rsp)
```


Why does this happen? While, according to the standard, the compiler is free to ignore the padding bytes, and do whatever it wants with it, for some reason it decides to not mess with it. 
It is free to do the second optimisation always, and fill the padding bytes with whatever favourite garbage it likes, but it chooses not to. Most likely because many developers might be wrongly using these padding bytes for optimisations (even though, they should not, and demons should be flying from their noses). But the compilers are polite, and still let you get away with it.

By forcefully doing the `memset`, the compiler knows, that these padding bytes will also be 0, so it can emit a single instruction, which writes all the 8 bytes at once!

> So... Are we done? Slap in a `memset` before populating every struct and your code is now 3 times faster, and bonuses 3 times larger?
{: .prompt-info }

Well not quite yet. As some of the wise people before me have said, always benchmark your optimisations...
The next developer comes around, and maybe decides, that we now need the flag to be an `int` instead of `char`
<pre><code class="language-cpp"> 
struct Packet {
    int id;
    int flag;
    uint16_t code;
};
</code></pre>

And running the same benchmark reveals, [that we are now 1.5 times slower!](https://quick-bench.com/q/Br-WKvYV_2yGOjS30pWnc_YnD2o) :(

So the bigger takeaway is to always benchmark.

Thank you![^cppcon]

[^cppcon]: I originally saw this optimization discussed in a CppCon talk but couldn’t find the exact video later. Please share a link in the comments, if you happen to find it. 






