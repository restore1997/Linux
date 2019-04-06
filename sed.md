### sed

```{shell}
sed "s/d/8/" nex.txt # 在nex.txt文本中将d替换成8
grep d nex.txt  #查找一下看看
grep 8 nex.txt
sed -n "s/d/8/p" nex.txt #-n选项和p命令一起使用表示只打印那些发生替换的行
sed -i "s/d/8/" nex.txt #直接编辑
sed  "s/8/9/g" nex.txt #替换每一行中的所有匹配
echo sksksksksksk | sed 's/sk/SK/2g' #当需要从第N处匹配开始替换时，可以使用 /Ng：
echo sksksksksksk | sed 's/sk/SK/3g'
sed '/^$/d' nex.txt #删除空白行
sed -i '/^$/d' nex.txt #编辑删除空白行
sed '2d' nex.txt
sed '2,$d' nex.txt #删除文件的第2行到末尾所有行
sed "$d" nex.txt # 注意单引号 ''
sed '/^test/'d file #删除文件中所有开头是test的行
echo this is a test line | sed 's/\w\+/[&]/g' #删除文件中所有开头是test的行
sed 's/^192.168.0.1/&localhost/' file #所有以192.168.0.1开头的行都会被替换成它自已加localhost
sed '表达式' | sed '表达式' #组合多个表达式
sed '表达式; 表达式' #同上
test=hello
echo hello WORLD | sed "s/$test/HELLO" #sed表达式可以使用单引号来引用，但是如果表达式内部包含变量字符串，就需要使用双引号。
sed -n '5,/^test/p' file #打印从第5行开始到第一个包含以test开始的行之间的所有行 
seq 1 1000|sed -n '4~4p' #打印4的倍数
sed '/test/,/west/s/$/aaa bbb/' file # 所有在模板test和check所确定的范围内的行都被打印
sed '/test/,/west/s/$/aaa bbb/' file #对于模板test和west之间的行，每行的末尾用字符串aaa bbb替换
sed -e '1,5d' -e 's/test/check/' file #在同一行里执行多条命令
sed '/test/r file' filename #file里的内容被读进来，显示在与test匹配的行后面，如果匹配多行，则file的内容将显示在所有匹配行的下面
sed -n '/test/w file' example #在example中所有包含test的行都被写入file里
sed '/^test/a\this is a test line' file #将 this is a test line 追加到 以test 开头的行后面
sed -i '2a\this is a test line' test.conf #将 this is a test line 追加到 以test 开头的行后面
sed '/^test/i\this is a test line' file  #将 this is a test line 追加到以test开头的行前面
sed -i '5i\this is a test line' test.conf  #在test.conf文件第5行之前插入this is a test line
sed '/test/{ n; s/aa/bb/; }' file  #如果test被匹配，则移动到匹配行的下一行，替换这一行的aa，变为bb，并打印该行，然后继续
sed '1,10y/abcde/ABCDE/' file #把1~10行内所有abcde转变为大写，注意，正则表达式元字符不能使用这个命令
sed '10q' file #打印完第10行后，退出sed
sed -n 'p;n' test.txt  #打印奇数行
sed -n 'n;p' test.txt  #偶数行
sed -n '1~2p' test.txt  #奇数行
sed -n '2~2p' test.txt  #偶数行
grep -A 1 SCC URFILE #打印匹配字符串的下一行
sed -n '/SCC/{n;p}' URFILE #打印匹配字符串的下一行
awk '/SCC/{getline; print}' URFILE #打印匹配字符串的下一行
seq 1 20|sed 's/2/2\t$/' #??

 zless ~/project/1.rna/3.part_clean_data/SRR1039510_1_val_1.fq.gz |paste - - - - |cut -f 2|grep -i -o [ATCGN]|wc
 zless ~/project/1.rna/3.part_clean_data/SRR1039510_1_val_1.fq.gz |paste - - - -|cut -f 2 |awk '{sum+=length($0)} END {print sum}'
```

