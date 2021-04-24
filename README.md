# Notes for missing semester in MIT
## Lecture 1
1. `date`
2. `echo hello`
3. `mkdir 'My Photos'` or `mkdir "My Photos"` or `mkdir My\ Photos` 如果直接`mkdir My Photos`将创立'My'和'Photos'两个目录。
4. `echo $PATH`
5. `which echo`
6. `pwd`
7. `cd home`,`cd ..`
8. `ls` `ls -l`
9. `man ls`
10. `< file` and `> file` 
  > `echo hello > hello.txt`
  > `cat hello.txt`
  > `cat < hello.txt > hello2.txt`
11. `ls -l / | tail -n1`
12. `curl --head --silent google.com | grep --ignore-case content-length | cut --delimiter=' ' -f2`
13. `cat brightness`
14. `echo 1 | sudo tee brightness`
15. `xdg-open` in Linux or `open` in MacOS 给出一个文件名，然后这个命令就会用合适的程序打开它。
## Lecture 2
1. 
  > `foo=bar` 这里不要有空格，否则会无法生效
  > `echo $foo` 
2. 两种方法在shell中定义字符串
  > 用双引号：`echo "Hello"`
  > 用单引号：`echo 'World'`
  > `echo "Value is $foo"` 输出的是`Value is bar` 替换掉shell中foo变量的值
  > 如果用的是单引号`echo 'Value is $foo'`输出的是`Value is $foo`，单引号中的变量不会被替换
3. 定义函数
  > `vim mcd.sh`
  > ```
  >  mcd(){
  >    mkdir -p "$1"
  >    cd "$1"
  >  }
  > ```
  > 这里的"$1"相当于argv 提供的一个参数
  >  `source mcd.sh` 
  >
  > `mcd test`就会切换到已经创建好的test目录 
  > $0 - 脚本的名字
  >
  > $1 to $9 - 脚本的第一个到第九个参数
  >
  > $@ - 所有的参数
  >
  > $# - 参数的个数
  >
  > $? - 返回之前命令的状态码
  >
  > > 0表示一切正常，1表示没成功
  >
  > $$ - Process identification number (PID) for the current script
  >
  > !! - 复制上一条的命令。Entire last command, including arguments. A common pattern is to execute a command only for it to fail due to missing permissions; you can quickly re-execute the command with sudo by doing sudo !!
  >
  > $_ - 上条命令的最后一个参数. If you are in an interactive shell, you can also quickly get this value by typing Esc followed by .

4. `false || echo "Oops fail"`输出Oops fail 

   `true || echo "Oops fail"`则不会输出，这里是因为false的状态码是1，true的状态码是0，而||的作用就是当第一个不成立的时候判度第二个条件

5. `ture && echo "Oops fail" `同理

6. `false ; echo "This will always print"`无论执行什么，都可以通过

7. `foo=$(pwd)`

8. 过程替换

   >  `cat <(ls) <(ls ..)`先把ls这个目录中的输出放到临时比文件内，再对父目录如法炮制，然后把两个文件连接
   
9. ```sh
   echo "Starting program at $(date)" # Date will be substituted
   
   echo "Running program $0 with $# arguments with pid $$"
   
   for file in "$@"; do
       grep foobar "$file" > /dev/null 2> /dev/null
       # When pattern is not found, grep has exit status 1
       # We redirect STDOUT and STDERR to a null register since we do not care about them
       # 2> means the STDERR
       # -ne mean no equal
       if [[ $? -ne 0 ]]; then
           echo "File $file does not have any foobar, adding one"
           echo "# foobar" >> "$file"
       fi
   done
   ```

10. `ls *.sh`通配，能够搜索出所有含有任意字符，且以.sh为后缀的东西

11. `ls project?`  ?只会展开一个字符

12. 花括号的应用`convert image.png image.jpg` or `convert image.{png,jpg}`笛卡尔积

13. `touch {foo,bar}/{a..j}`

14. >  `touch foo/x bar/y`
    >
    > `diff <(ls foo) <(ls bar)`

15. python与shell进行交互

    > python script.py a b c
    >
    > ./scipt.py a b c
    
16. `shell check mcd.sh` 能给出warning以及语法错误

17. `tldr convert` or `tldr ffmpeg`能够获得关于如何调用命令的命令示例

18. 查找文件

    > `find  . -name src -type d`在当前目录递归查找文件
    >
    > `find . -path '**/test/*.py' -type f`这里的**可以匹配零个或多个目录名
    >
    > `find . -mtime -1`查找被修改过的文件，这里表示的是在最近一天被修改的东西
    >
    > `find . -name "*.tmp" -exec rm {} \`把所有tmp后缀的文件删除掉
    
19. `fd ".*py"`

20. `locate`查找文件系统中具有指定子串的路径，可以用过`updatedb`进行数据库的更新。

21. `grep -R foobar .`可以通过递归的方式找遍整个目录。

22. `rg "import requests" -t py ~/scratch`查找用了request库的python 代码

23. `rg "import requests" -t py -C 5 ~/scratch`查找用了request库的python 代码并显示上下5行

23. `ripgrep`

24. `rg -u --files-without-match "^#\!" -t sh`   `-u`是不忽略隐藏文件，`--files-without-match`打印出不匹配整个模式的内容,`"^#\!"`的意思是匹配行首由`#!`的内容，`-t sh`表示只搜索.sh的文件 

25. `rg "import requests" -t py -C 5 --stats ~/scratch` 中的`--stats`可以输出统计结果

26. 如何找到已经执行过的命令？

    > 1. 上箭头
    > 2. `history`
    > 3. `history 1 | grep convert`打印出历史记录中有convert的命令
    > 4. `Ctrl+R`按执行时间倒序搜索
    > 5. `fzf`模糊搜索工具，一个交互式的grep。`cat example.sh | fzf`通过管道连到`fzf`上。之后就可以实时的搜索。如果打开默认绑定，它会绑定到shell的`Ctrl+R`执行上，就可以动态的查看。
    > 6. `fish` 和 `zsh`

27. 快速搜索目录命令

    > `ls -R`递归列出目录结构,`tree`，`broot `, `nnn`

## Lecture 3 Vim

Vim是基于模式（Modal）的编辑器。 **normal** 模式进入**insert**模式通过输入`i`进入，而**insert**模式进入**normal**模式通过`Esc`进入。**normal**模式用来移动光标，阅读东西以及文件间切换，**insert**模式则用来输入。还有**replace**模式，不会像插入模式会把字符往后移。**selection**模式，**visual** 模式(-line,-block)，从**normal**模式出发

> 按`i`进入insert模式 
>
> 按`R`进入replace模式
>
> 按`v`进入visual模式
>
> 按`shift-v`进入visual -line模式
>
> 按`Ctrl-V`进入visual-block模式
>
> 按`:`进入command-line模式

1. 保存文件，进入**command-line**模式输入`w`
2. 退出文件，进入**command-line**模式输入`q`
3. `:wq`保存并退出
4. `:e{name of file}`打开文件并编辑
5. 可以通过`:sp`来创建两个不同的窗口，打开的是同一个文件，通过`:sp`打开多个窗口后，就可以通过`:q`退出一个页面，也可以通过`:qa`退出所有的页面
6. 可用`：newtab`来新建立一个窗口
7. 移动光标：

> 1. vim的接口本身就是一个编程语言，不同的按键组合具有不同的效果，在Vim中用hjkl键，h左移，j下移，k上移，l右移
> 2. `w`和`b`键用来一个一个单词的移动
