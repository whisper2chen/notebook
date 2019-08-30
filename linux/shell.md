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
