## 一、说明

1. MAC系统采用Unix文件系统，所有文件都挂在根目录下面，没有Windows系统的盘符概念，根目录用斜杠(`/`)表示；
2. 根目录(`/`)不是可有可无，`/System`表示根目录下的System文件，`System`表示当前目录下的System文件；
3. 在 Unix系统中区别字符大小写，A.txt 不等于 a.txt；
4. 关键的标点符号：点(`.`)表示当前目录；两个点(`..`)表示上一级目录；星号(`*`)匹配任意字符任意次数；问号(`?`)匹配任意字符仅一次；
5. 获得权限：为了防止误操作破坏系统，再用户状态下没有权限操作重要的系统文件，先要获取root权限，语法：`sudo -s`，然后会提示输入密码，输入密码时没有任何回显，连星号都没有，输入完密码按回车键即可；
6. 编辑文件：`vim directory/file_name`，若指定路径的文件不存在，则新建空文件，输入字母`i`或`o`进入编辑模式，编辑好内容，点击【esc】键后，输入`:w`进行保存；输入`:wq`进行保存并退出；输入`:q!`进行不保存强行退出；
7. table键，单击可以实现自动补全，双击可以列出指定路径下的所有内容，类似`ls`命令；
8. 常用位置
    驱动所在位置： `/Systme/Library/Extensions`
    用户文件夹位置：`/User/用户名`，可以用波浪号(`~`)表示
    桌面位置：`/User/用户名/Desktop`，可以用`~/Desktop`表示
9. 清理系统
    按天进行清理：`sudo periodic daily`
    按每周进行清理：`sudo periodic weekly`
    按每月进行清理：`sudo periodic monthly`
    按上面3种情况进行清理：`sudo periodic daily weekly monthly`

## 二、目录和文件操作

|      命令名       | 功能描述                     | 举例或备注                       |
| :---------------: | ---------------------------- | -------------------------------- |
|        cd         | 进入指定文件夹路径           | cd ~/Desktop                     |
|        pwd        | 显示当前的目录路径           | /Users/xz/Desktop                |
|        ls         | 显示当前目录下的内容         |                                  |
|      ls -la       | 显示当前目录下的详细内容     |                                  |
|       ls -A       | 显示当前目录下的内容         | 含点(`.`)开头的文件              |
|       mkdir       | 创建目录                     | mkdir dir_name                   |
| touch file.format | 创建指定格式的文件           |                                  |
|       mvdir       | 移动目录                     | mvdir dir1 dir2                  |
|        mv         | 移动/重命名---文件/文件夹    | mv dir1 dir2 MAC没有重命名的命令 |
|        rm         | 删除文件 或 **空**目录       |                                  |
|    rm -rf dir     | 删除一个 **非空** 目录       | rm -rf dir                       |
|       rmdir       | 删除 **空** 目录             | 平时用得少                       |
|        cp         | 复制文件或目录               | cp file1 file2                   |
|       file        | 显示文件类型                 | file file_name                   |
|       find        | 使用匹配表达式查找文件       | find *.file_format               |
|       open        | 使用默认的程序打开文件       | open file_name                   |
|        cat        | 显示或连接文件内容           | cat file                         |
|        ln         | 为文件创建联接               | ln -s file1 file2 s 表示软联接   |
|       head        | 显示文件的最初几行           | head -20 file_name               |
|       tail        | 显示文件的最后几行           | tail -10 file_name               |
|       paste       | 横向拼接文件内容             | paste file1 file2                |
|       diff        | 比较并显示两个文件的内容差异 | diff file1 file2                 |
|        wc         | 统计文件的字符数、词数和行数 | wc file_name                     |
|       uniq        | 去掉文件中的重复行           | uniq file_name                   |
|       grep        | 通过简单正则表达式搜索文件   |                                  |

## 三、文件属性

- Linux系统：一切设备都可以看成是文件。如：目录、磁盘文件、管道、网络Socket、外接U盘和SD卡等；
- 文件属性：用户组、读、写、执行权限；
- 查看文件属性



```ruby
XZ:ts xz$ ls -l
total 82488
-rw-r--r--@ 1 xz  staff  42233727  7 19 16:30 PowerBi.pbix
```

|     语法     |   属性   | 含义说明                                    |
| :----------: | :------: | :------------------------------------------ |
|      -       | 文件类型 | 横杠表示普通文件，若为`d`表示文件目录       |
|  rw-r--r--   | 访问权限 | 分3组：用户、群组和其他用户的文件访问权限； |
|      1       | 文件数量 | 本例中仅1个文件                             |
|      xz      | 所在用户 | 本例中用户名为xz                            |
|    staff     | 所在群组 | 本例中用户群组为staff                       |
|   42233727   | 文件大小 | 本例中文件的字节数                          |
|  7 19 16:30  | 修改日期 | 本例中为7-19 16:30                          |
| PowerBi.pbix | 文件名称 | 本例中为PowerBi.pbix                        |

- 修改访问权限
   **语法**：`chmod 用户 操作 权限 文件`
   **用户**：`u`表示用户(user)、`g`表示群组(group)、`o`表示其他用户(other)、
     `a`表示全部用户。缺失的情况下默认为所有用户；
   **操作**：`+`表示增加权限、`-`表示取消权限、`=`表示赋值权限；
   **权限**：`r`表示可读(read)、`w`表示可写(write)、`x`表示可执行(execute)；
   **文件**：不指定文件名时，操作对象为当前目录下的所有文件。
- 示例：为user用户增加执行的权限



```ruby
XZ:ts xz$ chmod u+x PowerBi.pbix 
XZ:ts xz$ ls -l
total 82488
-rwxr--r--@ 1 xz  staff  42233727  7 19 16:30 PowerBi.pbix
```

## 四、常用操作

|     命令名     | 功能描述                     | 举例或备注                                                   |
| :------------: | ---------------------------- | ------------------------------------------------------------ |
|      sudo      | 获取root权限                 | sudo -s                                                      |
| Ctr + D / exit | 退出root权限                 |                                                              |
|     clear      | 清除屏幕或窗口内容           |                                                              |
|      ping      | 给网络主机发送回应请求       | ping [www.baidu.com](https://links.jianshu.com/go?to=http%3A%2F%2Fwww.baidu.com) |
|      man       | 查看命令说明                 | man ls                                                       |
|       q        | 退出查看的命令说明           |                                                              |
|     which      | 查看指定程序的路径           | which python                                                 |
|    history     | 列出最近执行过的命令及编号   |                                                              |
|    hostname    | 电脑在网络中的名称           |                                                              |
|      env       | 显示当前所有设置过的环境变量 |                                                              |
|     passwd     | 修改用户密码                 |                                                              |
|      date      | 显示系统的当前日期和时间     | date                                                         |
|      cal       | 显示日历                     | cal                                                          |
|      time      | 统计程序的执行时间           | time                                                         |

## 五、快捷键

- CTRL+A：移动光标至行首
- CTRL+E：移动光标至行尾
-  CTRL+X：按住CTRL，双击 X 可以进行当前位置与行首位置，进行切换
-  ESC+B：光标向左移动一个单词
-  ESC+F：光标向右移动一个单词
-  CTRL+U：删除光标前所有字符
-  CTRL+K：删除光标后所有字符
-  CTRL+W：删除光标前一个单词（根据空格识别单词分隔）
-  CTRL+Y：粘贴之前（CTRL+U/K/W）删除的内容
-  CTRL+C：中断操作

