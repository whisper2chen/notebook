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
```
