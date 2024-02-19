# EDGE CASES

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

## 🚀 WHAT ARE EDGE CASES ?

During my `minishell` project, I went through some Github testers, most of them are *happy paths* tests.

Unfortunatelly (*for us*), `bash` treat every cases regardless of your feelings or emotions.

My goal here is trying to list as much prompts that I tested along the way of building `minishell`.

Some of them makes sense, some of them helped me grasp a better sense of what's `bash`.

Sometimes, ***meh*** 🤷 prompts doesn't makes sense at all...


I'll provide a few explanations on specific commands, a few insights sometimes...

> [!CAUTION]
> Keep in mind that some commands will **crush your soul and destroy your will to live with the efficiency of a bulldozer**.



> 🤔 Does it means that my `minishell` is rubish for not handling a specific edge case ?

Well, not necessarly. My minishell **sucks**, yours maybe a little more or a little less, but you're not supposed to handle everything !

> 🤔 Where do I draw the line between edges cases ?

Well, you chosse. Handle everything asked in the subject is a good start. Draw the line yourself, and ✨enjoy the process✨.

Keep in mind that I consider a **INVALID COMMAND** a command that have no consequence or have a undefined behaviour regarding of the `minishell` project.

| Prompt | Valid Input | Invalid Input | Note |
|--------|---------------|-----------------|--------|
|   `\|`   |  - | 🚫  |     |
|   ```\|\|\|\|\|\|\|```  |  - | 🚫  |     |
|   `><<>\|>\|><>>\|`   |  - | 🚫  |     |
|   `iwjegrfikwregk`   |  - | 🚫  |     |
|   `erngkjdnsreg \| echo bonjour \| rev`   |  ✅ |   |  Outputs an error message AND `ruojnob`   |
|   `e'c'"h"'o' b"onj"'o''u''r'`   |  ✅ |   |  Outputs `bonjour`   |
|   `>`   | -  | 🚫  |     |
|   `<`   |  - | 🚫  |     |
|   `>>`   | -  | 🚫  |     |
|   `<<`   |  - | 🚫  |     |
|   `> test`   |  ✅ | -  |     |
|   `> test \| echo bonjour`   |  ✅ | -  |     |
|   `> echo bonjour`   | -  | 🚫  |     |
|   `echo bonjour >`   |  - | 🚫  |     |
|   `echo bonjour > \| `   |  - | 🚫  |     |
|   `\| echo bonjour`   |  - | 🚫  |     |
|   `>> test`   |  ✅ |   |     |
|   `>> test \| echo bonjour`   |  ✅ | -  |     |
|   `>> echo bonjour`   |  - | 🚫  |     |
|   `echo bonjour >> `   |  - | 🚫  |     |
|   `echo bonjour >> \|`   |  - | 🚫  |     |
|   `echo bonjour \| rev \| >> test \| echo bonjour`   |  ✅ | -  |  create an empty file called `test`, DOES NOT erase his content if it does exists, outputs `bonjour` from the second echo   |
|   `< existing_file`   |  ✅ | -  |   |
|   `< not_existing_file`   |  - | 🚫  |     |
|   `< existing_file not_existing_file`   |  ✅ | -  |     |
|   `< not_existing_file existing_file`   |  - | 🚫  |     |
|   `< existing_file \| echo bonjour`   |  ✅ | -  |     |
|   `<< wlrgnjbeddfvdkrtfn \| echo bonjour`   |  ✅ | -  |    |
|   `<<  EOF \| echo bonjour \| rev`   |  ✅ | -  |     |
|   `<< EOF wrigjeriju \| echo bonjour`   |  ✅ | -  |     |
|   `echo $0`   |  ✅ | -  |  Outputs `bash`   |
|   `echo bonjour \| rev > test test test test`   |  ✅ | -  |     |
|   `echo $?`   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |
|   ``   |  ✅ | 🚫  |     |



