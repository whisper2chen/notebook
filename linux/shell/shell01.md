# linux shell 脚本攻略笔记
## 第1章
### 1.1
bash在sh的基础上扩展了功能，可以说sh是bash的子集 两者是兼容的<br>
> 注意ubuntu中sh是dash的符号连接 所以最好使用 #!/bin/bash 作为Sharp Bang
### 1.2
1. login shell 与 non login shell
> login shell是登陆linux时输入认证信息后取得的shell 它会读取.bash_profile文件<br>
> non login shell是之后执行比如bash后创建的shell  它只会读取.bashrc
2. echo
> 常用的参数<br>
```Shell
echo -e "hello\tworld" # -e 参数指定转义字符串
echo -E "hello\tworld" # -E 参数不指定转义字符串
echo -n "hello world"  # echo默认会输出换行符 -n指定不输出换行符
```
> 双引号与单引号<br>
```Shell
MYNAME="CHEN"
echo "my name is ${MYNAME}" # shell会解释双引号中的特殊值
echo 'my name is ${MYNAME}' # shell输出plain text
```
3. printf
> printf "%-5s %-10s %-4.2f" No1 Tom 98.675 # -指定左对齐 数字指定对齐长度

4. colorfull output
> 文本颜色
```
\e[0m 重置
echo -e "\e[1;30m黑色\e[0m"
echo -e "\e[1;31m红色\e[0m"
echo -e "\e[1;32m绿色\e[0m"
echo -e "\e[1;33m黄色\e[0m"
echo -e "\e[1;34m蓝色\e[0m"
echo -e "\e[1;35m洋红色\e[0m"
echo -e "\e[1;36m青色\e[0m"
echo -e "\e[1;37m白色\e[0m"
```
> 背景颜色
```
echo -e "\e[1;40m黑色\e[0m"
echo -e "\e[1;41m红色\e[0m"
echo -e "\e[1;42m绿色\e[0m"
echo -e "\e[1;43m黄色\e[0m"
echo -e "\e[1;44m蓝色\e[0m"
echo -e "\e[1;45m洋红色\e[0m"
echo -e "\e[1;46m青色\e[0m"
echo -e "\e[1;47m白色\e[0m"
```
5. 变量与环境变量
> varName=value<br>
> 等号前后没有空格.<br>
> value如果包含空格 则用引号括起来.<br>
> $varName ${varName}获取变量值.<br>
> ${#varName}获取字符值长度.<br>
> 惯例：变量以小写驼峰命名  环境变量以大写字母命名.<br>
> export varName 可以是变量变成环境变量,环境变量在父子进程之间共享.<br>
> 进程的environment 可以通过读取/proc/$PID/environ 查看(字段以\0分割).<br>
```Shell
cat /proc/$PID/environ | tr '\0' '\n' #以换行符分割
```

6. shell参数扩展
> ${parameter:+expression}<br>
> #parameter不为空 则取expression的值.<br>
> #parameter为空 则取parameter的值 即空.<br>
--------------------------
> ${parameter:-expresion}<br>
> #parameter不为空 则取parameter的值.<br>
> #parameter为空 则取expression的值.<br>
--------------------------
> ${parameter:=expersion}<br>  
> #parameter不为空 则取parameter的值<br>
> #parameter为空 则取expersion的值 且将expression值赋值与parameter.<br>
--------------------------
> ${parameter:?expersion}<br>  
> #parameter不为空 则取parameter的值<br>
> #parameter为空 则打印expression并终止退出.<br>

7. shell数学运算
> $((1 + 2))  # $(())用于计算整型的值
> 浮点运算使用bc
```Shell
echo "3.14 * 8 ^ 2" | bc
echo "scale=10;10/3" | bc #scale指定计算精度
echo "obase=2;100" | bc #二进制输出值
```

8. shell管道
```Shell
#<表示stdin
#>表示stdout
#2>表示stderr
#管道传输默认是标准输出
# cmd1 2>&1 | cmd2 可以重定向stderr 到管道
# cmd1 > /dev/null 2>&1 可以重定向到null设备 什么都不输出
# cmd1 | tee file   可以同时输出到stdout和file中

$ cat text.txt
1
2
3
$ out=$(cat text.txt)
$ echo $out
1 2 3 #  丢失了1 、2 、3 中的\n
$ out="$(cat text.txt)"
$ echo $out
1
2
3
```

9. 数组与关联数组
数组<br>
```Shell
array=(item1 item2 item3 item4)
echo ${array[0]}   #打印第一个元素
echo ${array[*]}   #打印所有元素
```
关联数组<br>
从bash 4.0之后开始支持<br>
```Shell
declare -A array
array[key1]=value1
array[key2]=value2
echo ${array[key1]}
echo ${!array[*]}  #打印所有的key值
```

10. 终端控制
```
stty -echo #取消终端的回显
stty echo  #打开回显

tput sc    #记录光标位置
tput rc    #返回之前记录的光标位置
tput ed    #删除当前光标位置到行尾的所有内容
```

11. date
```Shell
date +%s #打印时间戳
date -d "2019-8-31 8:54" +%s  #转换字符串表示的时间
date -d @1567212893           #转换时间戳到字符串表示
```

12. 脚本调试
```Shell
bash -x test.sh #调试的信息会默认输出到stderr

#也可以在脚本中在想调试的部分
set -x
some block to debug
set +x
```

13.  函数
```Shell
function f() {
  echo -n "something to output"
}

echo $(f)   #调用函数
```

14. read
```
(1) 下面的语句从输入中读取n个字符并存入变量 variable_name ：
read -n number_of_chars variable_name
例如：
$ read -n 2 var
$ echo $var
(2) 用无回显的方式读取密码：
read -s var
(3) 使用 read 显示提示信息：
read -p "Enter input:" var
(4) 在给定时限内读取输入：
read -t timeout var
例如：
$ read -t 2 var
# 在2 秒内将键入的字符串读入变量var
(5) 用特定的定界符作为输入行的结束：
read -d delim_char var
例如：
$ read -d ":" var
hello: #var 被设置为hello
```
