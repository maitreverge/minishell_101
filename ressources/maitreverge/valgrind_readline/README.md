# IGNORING READLINE LEAKS

## 🚀 WHAT IS READLINE ?

The `readline` function is the entry door for your `minishell` program ! It is basically a `char *` buffer where your prompt will end up.

The `readline` function in C is part of the GNU Readline library, which is known to have some internal memory management that can appear as a memory leak when analyzed with tools like Valgrind.

## 🤔 VAL_what ?

From now, you should be familiar with `valgrind`. It's either our closest friend or worse nightmare, especially when writting buggy C code at 42 !

Valgrind is an open-source tool that helps detect memory management issues in programs, such as memory leaks, use of uninitialized memory, and inappropriate read/writes.
It operates by running your program in a controlled environment and reporting any problems it encounters, making it a powerful tool for finding and fixing memory-related bugs.


## HOW TO SUPPRESS `readline` LEAKS ?

When building your minishell, you may have noticed that no matter how perfect is your minishell, it is still leaking when running `valgrind`.

I'll give you a glance of what valgrind throws at me :

``` bash
valgrind ./minishell
```

```
==44201== HEAP SUMMARY:
==44201==     in use at exit: 228,668 bytes in 239 blocks
==44201==   total heap usage: 877 allocs, 639 frees, 259,274 bytes allocated
==44201== 
==44201== LEAK SUMMARY:
==44201==    definitely lost: 36 bytes in 2 blocks
==44201==    indirectly lost: 0 bytes in 0 blocks
==44201==      possibly lost: 0 bytes in 0 blocks
==44201==    still reachable: 228,632 bytes in 237 blocks
==44201==         suppressed: 0 bytes in 0 blocks
==44201== Rerun with --leak-check=full to see details of leaked memory
==44201== 
==44201== For lists of detected and suppressed errors, rerun with: -s
==44201== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)

```

As you can see, my program actually leaks 36 bytes (*yeah I know*)... but actually **238,632** are still reachable ?

We can't do anything about leaks from `readline`, the goal here it to tell valgrind ***Hey, turn `readline` leaks in a specific place which I can clearly indeitfy***

## 🧙 HERE'S THE SPELL

At your root repository, create a file called `valgrind.supp`

> [!NOTE]  
> `valgrind.supp` is a convention name that have nothing to do with the functionality itself. Name it as you wish.

Next, enter in this file :

```
{
   ignore_libreadline_leaks
   Memcheck:Leak
   ...
   obj:*/libreadline.so.*
}
```
