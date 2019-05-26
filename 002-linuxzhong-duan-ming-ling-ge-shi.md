#### 一、Linux 终端命令格式

**01、终端命令格式**
```
command [-option] [parameter]
```
**说明: **
- `command` 命令名
- `-option` 选项, 可以用来对命令进行控制, 也可以省略
- `parameter` 传给命令的参数, 可以是0个, 也可以是一个或多个


<br>
**02、Linux 中查看命名帮助的方式**
- 方式1:  显示`command`命令的帮助信息
```
command --help
```

- 方式2: 查看 `command`命令的使用手册
```
man command  // man 是manual 的缩写(手册的意思)
```

**使用 `man` 命令是的操作**

|操作|功能描述|
|-|-|
|空格键|显示手册的下一屏|
|enter键|一次滚动手册页的一行|
|b| 回滚一屏|
|f|前滚一屏|
|/word| 搜索 word 字符串|
