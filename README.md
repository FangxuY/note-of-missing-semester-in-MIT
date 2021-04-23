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
