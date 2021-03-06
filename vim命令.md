# vim命令说明

## 退出

:q  退出

:q! 不保存退出

:wq 保存并退出

## 保存

:w 保存

:w filename 另存为

:(#,#) w filename 另存(两行间内容)为

## 插入

:r filename 提取磁盘文件并将其插入到当前光标位置

o 在光标下方打开新的一行并将光标置于新开的行首，进入插入模式

O 在光标上方打开新的一行并将光标置于新开的行首，进入插入模式

a 可以在光标所在位置之后插入文本

A 可以在光标所在行的行末之后插入文本

## 复制粘贴

yy 复制

yw 复制单词

p 粘贴到下一行(将最后一次删除的内容置入光标之后)

P 粘贴到上一行

## 删除

x 删除

[number]   d    object ||  d    [number]   object

dw 从当前光标当前位置直到单字/单词末尾，包括空格

de 从当前光标当前位置直到单字/单词末尾，不包括空格

d$ 从当前光标当前位置直到当前行末

dd 删除整个当前行

## 行尾

:%s/\n//g 删除换行符

J 连接该行与下行，删除行尾的换行符 

:join 合并多行

# 撤销

u 撤消最后执行的(一次)命令

U 撤消在一行中所做的改动

CTRL-r 欲撤消以前的撤消命令，恢复以前的操作结果

# 查找

/+字符串 在当前文件中查找该字符串
 
?+字符串  逆向查找字符串

:set ic  忽略大小写ignore case

:set hls is 高亮查找hlsearch 和 incsearch

% 可以查找配对的括号 )、]、}

n 下一个

Shift-n(N) 上一个

# 替换

:s/old/new  本行首个替换（在一行内替换头一个字符串 old 为新的字符串 new ）

:s/old/new/g 本行全行替换（在一行内替换所有的字符串 old 为新的字符串 new）

:%s/old/new/g 全文全行替换（在文件内替换所有的字符串 old 为新的字符串 new）

:%s/old/new/gc 全文全行替换，询问用户确认每个替换

:#,#s/old/new/g 在两行内全行替换所有的字符串 old 为新的字符串 new

:.,s/sgd/lbfgs/g本行到末行全行替换:n,

s/sgd/lbfgs/g   第n行到末行全行替换

# Insert模式

r* 替换光标所在位置的字符

R*** 进入替换模式，直至按 <ESC> 键退出替换模式而进入正常模式。

[number]   c    object ||  c    [number]   object

cw** 不仅仅是替换了一个单词，也让您进入文本插入状态

c$ 替换从当前光标当前位置直到当前行末

# 特殊字符

:set list 显示以“$”表示的换行符和以“^I”表示的制表符

:set nolist 退出<list mode>

# 信息

CTRL-g 页面最底部出现状态信息行，显示文件名、总行数、行号。

:set nu 显示行号

:set nonu 隐藏行号

# 光标

G 使得当前光标直接跳转到文件最后一行

"#G"  跳转到#行（输入行号时，行号是不会在屏幕上显示出来的）

# 外部命令
:!+shell命令  如:!rm filename

# 可视化
ctrl+v   可视化

shift+v 复制多行

shift+i  注释多行

# 配置
Vim的功能特性要比vi多得多，但大部分功能都没有缺省激活。为了启动更多的功能，您得创建一个vimrc文件。

1. 开始编辑vimrc文件，这取决于您所使用的操作系统∶

     :edit ~/.vimrc   这是Unix系统所使用的命令
     :edit $VIM/_vimrc   这是Windows系统所使用的命令

2. 接着导入vimrc范例文件∶:read $VIMRUNTIME/vimrc_example.vim

3. 保存文件，命令为:write

 在下次您启动vim的时候，编辑器就会有了语法高亮的功能。您可继续把您喜欢的其它功能设置添加到这个vimrc文件中。