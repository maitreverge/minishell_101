# IGNORING READLINE LEAKS

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

## 🚀 WHAT IS READLINE ?

The `readline` function serves as the entry point for your minishell program! It essentially acts as a `char *` buffer where your prompt will ultimately end up.

The `readline` function in C is part of the GNU Readline library, which is known to have some internal memory management that can appear as a memory leak when analyzed with tools like Valgrind.

## 🤔 VAL_what ?

By now, you should be familiar with `valgrind`. It's either our closest friend or worse nightmare, especially when writting buggy C code at 42 !

Valgrind is an open-source tool that helps detect memory management issues in programs, such as memory leaks, use of uninitialized memory, and inappropriate read/writes.

It operates by running your program in a controlled environment and reporting any problems it encounters, making it a powerful tool for finding and fixing memory-related bugs.


## HOW TO SUPPRESS `readline` LEAKS ?

While building your minishell, you may have noticed that no matter how perfect is your minishell, it is still leaking when running `valgrind`.

I'll give you a glimpse of what valgrind throws at me :

``` bash
valgrind ./minishell
```
Here's the output :

``` python
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

As you can see, my program actually leaks 36 bytes by my fault (*Yeah I know... sue me*)...

but actually **238,632 bytes** are still reachable ?

We can't do anything about leaks from `readline`, the goal here it to tell valgrind something like

> ***Hey, turn `readline` leaks in a specific place which I can clearly identify***



## 🧙 HERE'S THE SPELL

### STEP 1 : Create a Valgrind Suppression File

At your root repository of your minishell project, create a file called `valgrind.supp`

> [!NOTE]  
> `valgrind.supp` is a convention name that has nothing to do with the functionality itself. Name it as you wish.

Next, enter in this file :

```
{
   ignore_libreadline_leaks
   Memcheck:Leak
   ...
   obj:*/libreadline.so.*
}
```

🎊 **CONGRATULATIONS** 🎊

You just wrote a    😎 **Valgrind Suppression File** 😎

In simpler term, this rule tells `valgrind` to ignore any memory leaks that come from the `libreadline` library, no matter where in your code the memory was allocated.

### STEP 2 : Using a Valgrind Suppression File

Now that you created your file `valgrind.supp`, you need to adress this file to `valgrind` with a special flags which is

``` bash
valgrind --suppressions=valgrind.supp ./minishell
```
Here is the valgrind output this time :
``` python
==44683== HEAP SUMMARY:
==44683==     in use at exit: 228,668 bytes in 239 blocks
==44683==   total heap usage: 871 allocs, 633 frees, 259,234 bytes allocated
==44683== 
==44683== LEAK SUMMARY:
==44683==    definitely lost: 38 bytes in 2 blocks
==44683==    indirectly lost: 0 bytes in 0 blocks
==44683==      possibly lost: 0 bytes in 0 blocks
==44683==    still reachable: 16 bytes in 1 blocks
==44683==         suppressed: 228,614 bytes in 236 blocks
==44683== Rerun with --leak-check=full to see details of leaked memory
==44683== 
==44683== For lists of detected and suppressed errors, rerun with: -s
==44683== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
```

Notice that without this tool, I wouldn't be able to track another 16 bytes that have been mixed with `readline` leaks...

Which now are on a new line `suppressed`.

You did not have really suppressed them, you have "moved" them.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

I hope this little guide helped.

Special thanks to [Floperatok](https://github.com/Floperatok) for giving me insights on this one and digging up on StackOverFlow !

🚀 Happy coding !
