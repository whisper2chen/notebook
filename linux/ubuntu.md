# i :heart: 命令行





### find
```sh
find . -name "*.txt" -ok rm {} \;   #-ok删除文件的时候带确认
find . -name "*.txt" -exec rm {} \; #直接删除找到的文件
```


### grep
```sh
cat err.log | grep error -A 5 -B 5  #查看error 并显示error处前后5行
```
