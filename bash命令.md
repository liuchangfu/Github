# bash命令

##目录
 
pwd //查看当前目录

mkdir dir1 dir2 //创建目录

tree dir1

mv test1.cpp test2.cpp dir1 dir  //移动文件/目录到目录dir 

rm -r dir         删除目录

cp -r dir1 dir2 复制目录 

##文件信息

ll –t //列出详细信息，按时间排序

ls -R(ecursive) 目录树 -l 详细信息 -t 时间排序 -S 大小排序 -X 扩展名排序 -r(everse) 逆序 –h(uman) 大小以G/M为单位 –m 以M为单位 -a 列出包括隐藏文件 

wc -l *.txt //看文件行数

du -sm * | sort -n //统计当前目录下文件及文件夹大小（以M为单位），并按大小排序 

touch test1.cpp test2.cpp //将每个文件的访问时间和修改时间改为当前时间

Change the mode of each FILE to MODE.
With --reference, change the mode of each FILE to that of RFILE.

##文件内容

cat file  //看文件内容

more file //从开始看，空格下一屏

tail -n 20 file //看最后n行，默认十行

tail -f file  //看日志时用，会刷新

##压缩文件

tar –f 生成文件 目标文件
-f(ile) 必选 
-c creat压缩(默认)
-x eXtra解压
-j 使用压缩算法-bzip算法bz2
-z 使用压缩算法-gzip算法gz
–a(uto)  使用归档后缀名来决定压缩程序

tar -f archive.tar foo bar  # 从文件 foo 和 bar 创建归档文件 archive.tar。

tar -zf archive.tar.gz foo bar # 从文件 foo 和 bar 创建归档文件 archive.tar.gz。

tar -xf archive.tar          # 展开归档文件 archive.tar 中的所有文件。

tar –tf –v(erbose) archive.tar    # test-label 详细列举归档文件 archive.tar 中的所有文件。 

*.gz //gzip程序压缩的文件

*.bz2 //bzip2程序压缩的文件（比gzip效果好，但只能针对一个文件来压缩）

*.tar //tar程序打包的数据，没有压缩（使用tar打包成一个文件，可以解决bzip2不能压缩多个文件的问题）

*.tar.gz  //tar程序打包的数据，并经过gzip的压缩

*.tar.bz2 //tar程序打包的数据，并经过bzip2的压缩 

zip -r ./src.zip ./*  //压缩文件

unzip text.zip -d . //解压到当前目录

unzip -v text.zip  //查看压缩文件目录，但不解压

bzip2 text.txt –f(orce) overwrite existing output files //压缩文件

bunzip2 text.txt.bz2 –k(eep)  keep (don't delete) input files //解压文件

bzcat *.bz2 或者 bunzip2 –c *.bz2 //解压文件到 stdout

##拷贝文件

cp –i(nteractive) -r idirectory odirectory 拷贝文件夹i到文件夹o，覆盖前询问

scp -r work@XXXX:~/maxent_test/ ./st  主机之间安全拷贝文件，通过ssh协议传输

sz和rz传小文件大概10kb/s还行，大文件太慢了

##下载文件

wget url 下载 -q 关闭输出

##移动文件

mv /usr/local/arm/arm/* /usr/local/arm/

##管道

ls | wc -l  将前一个命令的输出作为后一个命令的输入

##流

> < 重定向

<< 追加

echo string >> file 追加文件

##进程和任务

nohup cmd & 后台执行任务cmd 

jobs 查看（当前终端？不晓得）所有运行任务

ps x 查看所有进程信息 

renice [-10,+10] -p pid 设置进程优先级-10最高 

##grep

egrep "Test|Best arg|Final Eval Result"  letter/svm/*

grep -r(ecursive) -(in)v(ert) -(line-)n(umber) string file

grep "aaa" sample 文件下查找'aaa'

grep -r "aaa" .  目录下查找

grep -v "grep" sample 文件下查找非'grep'

grep -n "aaa" sample 显示行号

明确要求搜索子目录：grep -r

或忽略子目录：grep -d sk?ip?

grep magic /usr/src/linux/Documentation/* | less 许多输出，将其转到‘less’上阅读

grep -i pattern files ：不区分大小写地搜索。默认情况区分大小写

grep -l pattern files ：只列出匹配的文件名

grep -L pattern files ：列出不匹配的文件名

grep -C number pattern files ：匹配的上下文分别显示[number]行

grep pattern1 | pattern2 files ：显示匹配 pattern1 或 pattern2 的行

grep pattern1 files | grep pattern2 ：显示既匹配 pattern1 又匹配 pattern2 的行

grep -w pattern files ：只匹配整个单词，而不是字符串的一部分

grep man * 会匹配 ‘Batman’、‘manic’、‘man’等

grep '\<man' * 匹配‘manic’和‘man’，但不是‘Batman’

grep '\<man\>' 只匹配‘man’，而不是‘Batman’或‘manic’等其他的字符串

'^'：指匹配的字符串在行首

'$'：指匹配的字符串在行尾

##find 

find . -name '*.html' -exec grep 'mailto:' {} \;

find  \. -name \*.py -type f -exec echo {} \;   查找文件
-name /*.py

-type d(ir)/f(ile)

-size 1k 1k内文件

-exec

find path -option [ -print -exec -ok ...]

path ~=/home

-exec command {} \; 将查到的文件执行command操作,{} 和 \;之间有空格

-ok 和-exec相同，只不过在操作前要询用户

find -name "*.h"

     -prune 忽略某个目录

     -type b/d/c/p/l/f 查是块设备b、目录d、字符设备c、管道p、符号链接l、普通文件f

     -follow 如果遇到符号链接文件，就跟踪链接所指的文件

find /tmp -name "*.h" -exec grep "str" {} \; -print 在返回的文件list中查找str

find / -name '*.c'    -ok rm -rf {} \; 所有目录下查找并强制删除

find . -size +3000k   -exec ls -ld {} \;

-mmin nmkdir

查找系统中最后N分钟被改变文件数据的文件

-mtime n

查找系统中最后n*24小时被改变文件数据的文件

-mtime -n/+n

查找n天内或n天前修改的文件

-newer f1 !f2

查更改时间比f1新但比f2旧的文件

-amin n

查找系统中最后N分钟访问的文件

-atime n

查找系统中最后n*24小时访问的文件

-cmin n

查找系统中最后N分钟被改变文件状态的文件

-ctime n

查找系统中最后n*24小时被改变文件状态的文件

##Shell命令行

tab       // 补全

"#"          //注释

ctrl+a   //home

ctrl+e //end

ctrl+l 清屏

reset 清屏（处理卡在半个字符的情况）

history -n 100|grep svn //查找历史命令记录

ctrl+r svn //一直往前查找

ctrl+c 取消命令 

##其他

man MD5

man3 MD5

ln -s 软链接 source target

su 切换到root账户