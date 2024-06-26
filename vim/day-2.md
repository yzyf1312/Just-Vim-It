# [小试牛刀：行相关命令](./day-2.md#小试牛刀：行相关命令)

经过第一天的小试牛刀，这时候的你估计已经可以大概地操控光标了（可能还是不太习惯上下左右），但是不用担心，在接下来的每一天的训练里，你都会不断地重复巩固他们，直到它们变成你不假思索的动作。

今天，我们将更进一步，去学习更多更有用的操作；但在这之前，我想问你一个问题：

- 昨天的训练中，你是否发现，`h` `j` `k` `l` 固然可以移动光标，但是在很多时候，他们移动的效率实在是太慢了...；想想，当光标是在一行中的末尾，你却要修改行首的字符时，这就要一顿好按才行。而今天，我们就来尝试解决这个问题

## [移动光标到行首](./day-2.md#移动光标到行首)

1. 移动到光标所在行的第一个字符：`0`
2. 移动到光标所在行的除 `blank` 字符外的第一个字符：`^`

## [移动光标到行尾](./day-2.md#移动光标到行尾)

1. 移动到光标所在行的最后一个字符：`$`
2. 移动到光标所在行的除 `blank` 字符外的最后一个字符：`g _`

## [化繁为简](./day-2.md#化繁为简)

通过上面的四个操作，你就可以让你的光标快速去到行首行尾了；但是这时新的问题也随之而来，这四个操作，三个是需要击键两次，一个是需要那笨拙的右小拇指费劲按的键，光标的移动速度也一样是慢。这时我们就可以在 vscode 中对 vim 插件进行新键位映射，以简单化我们的使用；其中，`^` 和 `g _` 在开发中是很常用的，我们就对这两个操作进行重新映射。

在 `setting.json` 中添加设置：

```
"vim.normalModeKeyBindings": [
  {
    "before": ["H"],
    "after": ["^"]
  },
  {
    "before": ["L"],
    "after": ["g", "_"]
  }
],
```

通过这样设置，我们就可以使用 `H` `L` 来达到和 `^` `g _` 一样的效果了；其中，这里的 `vim.normalModeKeyBindings` 是指在 vim Normal 模式即命令模式下的键映射，对于其他模式（如插入模式及后面会学到的可视化模式）是不起作用的。对于往后我们有其他的操作觉得比较复杂但是又常用的，也可以通过这种方式来添加自己的配置。

## [一简再简](./day-2.md#一简再简)

通过键位的重新映射，总算是可以愉快地行首行尾快速输入了...吗？

并没有的。想想：光标跳到行首或行尾后，要输入字符的话，我们还是要再使用如 `i` `a` 这些操作指令，才能从命令模式进入输入模式；这时，我们就要请出新的操作命令了：

1. 在光标所在行行首插入(并进入输入模式)：`I`
2. 在光标所在行行尾插入(并进入输入模式)：`A`
3. 在光标所在行的上方插入空白行插入(并进入输入模式)：`O`
4. 在光标所在行的下方插入空白行插入(并进入输入模式)：`o`

通过这几个命令，我们就可以让光标快速跳到对应的位置并进入输入模式。

## [three more thing](./day-2.md#three-more-thing)

1. 复制光标所在行：`yy`；与系统的 `command + c` 不冲突，即如果先通过 `cmd + c` 复制一些内容，再通过 `yy` 复制一些内容，此时 `command + v` 快捷键粘贴出来的内容是 `command + c` 复制的内容而非 `yy` 复制的内容;
2. 粘贴：`p`；在 vim 中，有一个叫寄存器的概念，无论是 `y`（复制指令），还是 `d`（删除指令），`c`（删除并进入输入模式指令），被操作后的内容都会暂存在寄存器中，通过 `p` 指令则会把寄存器中的内容重新输出，从而达到粘贴的功能
3. 通过 `v` 可以选中内容，`h` `j` `k` `l` 调整选中区域，选中后通过 `y` 复制内容

>提示
>
>用完中文输入法后尽快切回英文模式