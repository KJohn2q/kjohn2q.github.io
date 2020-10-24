---
title: 'Keep file in a Git repo, but don''t track changes'
date: 2020-10-24 23:50:15
tags: ['git']
categories: tool
---

在工作中，我们常会使用 `git` 来进行项目的版本控制。但项目的一些配置文件我们希望只是存储在存储库中，本地开发环境对该部分配置文件进行修改，适合本地开发。而不将该部分修改提交到版本库。如：数据库配置文件。
那么怎样实现本地不追踪存储库中某文件的修改呢？有两种方法可以实现：

* `git update-index --assume-unchanged [filename]`
* `git update-index --skip-worktree [filename]`

那么这两种方法有什么区别呢？

`assume-unchanged` is designed for cases where it is expensive to check whether a group of files have been modified; when you set the bit, git (of course) assumes the files corresponding to that portion of the index have not been modified in the working copy. So it avoids a mess of stat calls. This bit is lost whenever the file's entry in the index changes (so, when the file is changed upstream).

`assume-unchange` 应用于检测一组文件是否修改成本很高的情况；当你设置了该选项，`git` 会假设在工作区副本中，索引对应的这部分文件没有修改。这避免了大量的`stat`的调用。每当文件在索引中的条目发生变化时，该选项无效。（也就是说当文件在上游发生变化时）

`skip-worktree` is more than that: even where git knows that the file has been modified (or needs to be modified by a reset --hard or the like), it will pretend it has not been, using the version from the index instead. This persists until the index is discarded.

`skip-worktree`不止于此：即使 `git` 监测到该文件发生了变化（或者当执行 `reset --hard` 文件需要发生变化），将会假装没有发生变化，而使用索引中的版本。直到索引被丢弃。

`--assume-unchanged` 假想开发者不应该修改该文件。该选项是为了提升那些像SDK一样不会修改的文件目录的性能。
`--skip-worktree` 当你指示 `git` 不要监测指定文件，因为开发应该修改该文件。例如，主存储库上游主机存储了一些应用于生产环境的配置文件，你不希望偶然间不小心提交对这些文件的修改, `--skip-worktree` 是你正想要的。

原文回答：[Git - Difference Between 'assume-unchanged' and 'skip-worktree'](https://stackoverflow.com/questions/13630849/git-difference-between-assume-unchanged-and-skip-worktree#)

引用链接：

* [Keep file in a Git repo, but don't track changes](https://stackoverflow.com/questions/9794931/keep-file-in-a-git-repo-but-dont-track-changes)
* [Git - Difference Between 'assume-unchanged' and 'skip-worktree'](https://stackoverflow.com/questions/13630849/git-difference-between-assume-unchanged-and-skip-worktree#)
* [Difference between git rm & git rm --cached](https://stackoverflow.com/questions/54575972/difference-between-git-rm-git-rm-cached)
* [git-update-index](https://git-scm.com/docs/git-update-index)
* [git assume unchanged vs skip worktree - ignoring a symbolic link](https://stackoverflow.com/questions/6138076/git-assume-unchanged-vs-skip-worktree-ignoring-a-symbolic-link)
* https://fallengamer.livejournal.com/93321.html