---
title: Different Ubuntu
date: 2018-06-04 21:46:06
tags: Ubuntu
categories: Linux
---

# git basic command #

- git add

- git status

- git push

- git commit

- git rm file  删除仓库和本地中的文件

- git rm --cached file  只从仓库中删除，但是本地磁盘还在

- git mv file_from file_to  是、文件改名

- git log

- git log -p -2  一个常用的选项是 -p，用来显示每次提交的内容差异。 你也可以加上 -2 来仅显示最近两次提交：

- git log --stat  如果你想看到每次提交的简略的统计信息，你可以使用 --stat 选项。

- git config



configure the user name and email

    $ git config --global user.name "youname"
    $ git config --global user.email youremail@example.com

git set up your editor

	$ git config --global core.editor emacs

check your configuration information

	$ git config --list
	user.name=John Doe
	user.email=johndoe@example.com
	color.status=auto
	color.branch=auto
	color.interactive=auto
	color.diff=auto


你可能会看到重复的变量名，因为 Git 会从不同的文件中读取同一个配置（例如：/etc/gitconfig 与 ~/.gitconfig）。 这种情况下，Git 会使用它找到的每一个变量的最后一个配置。


你可以通过输入 git config <key>： 来检查 Git 的某一项配置

	$ git config user.name
	John Doe


.gitignore 列出要忽略的文件模式 

文件 .gitignore 的格式规范如下：

所有空行或者以 ＃ 开头的行都会被 Git 忽略。
可以使用标准的 glob 模式匹配。
匹配模式可以以（/）开头防止递归。
匹配模式可以以（/）结尾指定目录。
要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。

所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。 星号\* 匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（?）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。 使用两个星号（\*) 表示匹配任意中间目录，比如`a/**/z` 可以匹配 a/z, a/b/z 或 `a/b/c/z`等。*


	
GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表，你可以在 [https://github.com/github/gitignore](https://github.com/github/gitignore) 找到它.

