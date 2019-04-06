### awk

```shell
# awk是一种编程语言，用于在linux/unix下对文本和数据进行处理。数据可以来自标准输入(stdin)、一个或多个文件，或其它命令的输出。
awk [options] 'script' var=value file(s)
awk [options] -f scriptfile var=value file(s)
awk -F fs   #fs指定输入分隔符，fs可以是字符串或正则表达式，如-F:
awk -v var=value   #赋值一个用户定义变量，将外部变量传递给awk
awk -f scripfile  #从脚本文件中读取awk命令
awk -m[fr] val   #对val值设置内在限制，-mf选项限制分配给val的最大块数目；-mr选项限制记录的最大数目。这两个功能是Bell实验室版awk的扩展功能，在标准awk中不适用。
awk 'BEGIN{ print "start" } pattern{ commands } END{ print "end" }' file #基本结构 三部分可选，任意部分都可不出现在脚本中
echo -e "A line 1\nA line 2" | awk 'BEGIN{ print "Start" } { print } END{ print "End" }'
echo | awk '{ var1="v1"; var2="v2"; var3="v3"; print var1,var2,var3; }' #当print的参数是以逗号进行分隔时，打印时则以空格作为定界符。

###awk内置变量
echo | awk '{ var1="v1"; var2="v2"; var3="v3"; print var1"="var2"="var3; }'
 echo -e "line1 f2 f3\nline2 f4 f5\nline3 f6 f7" | awk '{print "Line No:"NR", No of fields:"NF, "$0="$0, "$1="$1, "$2="$2, "$3="$3}' # NR表示记录数，在执行过程中对应于当前的行号。 NF表示字段数，在执行过程中对应于当前的字段数。
#Line No:1, No of fields:3 $0=line1 f2 f3 $1=line1 $2=f2 $3=f3
#Line No:2, No of fields:3 $0=line2 f4 f5 $1=line2 $2=f4 $3=f5
#Line No:3, No of fields:3 $0=line3 f6 f7 $1=line3 $2=f6 $3=f7
echo -e "line1 f2 f3n line2 f4 f5" | awk '{print $NF-1}'#打印出一行中的最后一个字段
echo -e "line1 f2 f3n line2 f4 f5" | awk '{print $(NF-1)}' #打印倒数第二个字段
echo -e"l hh hi ggf"|awk '{ print $2,$3 }' #打印第二、第三个字段 注意''单引号
awk 'END{ print NR }' nex.txt #统计行数

### 外部变量
seq 5 | awk 'BEGIN{ sum=0; print "总和：" } { print $1"+"; sum+=$1 } END{ print "等于"; print sum }' ##???
VAR=10000
echo | awk -v VARIABLE=$VAR '{ print VARIABLE }'#借助-v选项，可以将外部值（并非来自stdin）传递给awk
var1="aaa"
var2="bbb"
echo | awk '{ print v1,v2 }' v1=$var1 v2=$var2 #传递外部变量2
awk '{ print v1,v2 }' v1=$var1 v2=$var2 filename #输入来自于文件时

### 运算与判断
awk 'BEGIN{a="b";print a++,++a;}'# 0 2  所有用作算术运算符进行操作，操作数自动转为数值，所有非数值都变为0
a+=5 #等价于：a=a+5; 其它同类??
awk 'BEGIN{a=1;b=2;print (a>5 && b<=2),(a>5 || b<=2);}' ## || 或    && 与
awk 'BEGIN{a="100testa";if(a ~ /^100*/){print "ok";}}' # ~ 匹配正则表达式 ~！不匹配正则表达式
awk 'BEGIN{a=11;if(a >= 9){print "ok";}}' #< <= > >= != == 关系运算符
awk 'BEGIN{a="b";print a=="b"?"ok":"err";}' #??
awk 'BEGIN{a="b";arr[0]="b";arr[1]="c";print (a in arr);}' #??
awk 'BEGIN{a="b";arr[0]="b";arr["b"]="c";print (a in arr);}' #??

### awk高级输入输出
awk 'NR%2==1{next}{print NR,$0;}' text.txt #在循环逐行匹配，如果遇到next，就会跳过当前行，直接忽略下面语句。而进行下一行匹配。
awk 'BEGIN{ "date" | getline out; print out }' test #执行linux的date命令，并通过管道输出给getline，然后再把输出赋值给自定义变量out，并打印它
echo | awk '{printf("hello word!n") > "datafile"}'  #输出文件
echo | awk '{printf("hello word!n") >> "datafile"}' #输出文件

awk '{for(i=4;i<NF;i++)printf("%s ",$i);print $NF}' history1.txt #取第4列到最后一列
#在shell打完命令，用以上代码可以直接复制到markdown中，很方便。
seq 1 20|awk '$0%2==0{print $0}' # 打印2的倍数
seq 1 20|awk '{if($0%2==0)print $0}' #同上
```

