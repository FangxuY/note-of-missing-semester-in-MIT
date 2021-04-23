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
    > mcd(){
    >   mkdir -p "$1"
    >   cd "$1"
    > }
    > ```
