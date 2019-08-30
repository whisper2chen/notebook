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
