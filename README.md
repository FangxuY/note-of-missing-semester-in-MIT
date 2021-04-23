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
