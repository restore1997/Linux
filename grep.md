### grep

```{shell}
# grep（global search regular expression(RE) and print out the line，全面搜索正则表达式并把行打印出来）是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。
grep d nex.txt #在nex.txt文件中搜索d
grep "d" nex.txt #同上
grep d nex.txt his_20190317.txt #在多个文件中查找
grep -v d nex.txt #输出除之外的所有行 -v 选项
grep d nex.txt --color=auto #标记匹配颜色 --color=auto 选项：
grep -E "[1-9]" nex.txt #[]为正则表达式 在文件中搜索1到9
grep -E "[a-z]" nex.txt #搜索a到z
grep -E "[a-z]+" nex.txt #同上
echo this is a test line. | grep -o -E "[a-z]+\." #只输出文件中匹配到的部分 -o 选项 \为正则表达式 转义符，将特殊字符进行转义  如a\.b匹配a.b，但不能匹配ajb，.被转义为特殊意义
echo this is a test line. | grep  -E "[a-z]+\." #同上
grep -c "d" nex.txt #统计文件或者文本中包含匹配字符串的行数
cat nex.txt
grep -n "d" nex.txt #输出包含匹配字符串的行数
cat nex.txt|grep -n "d" #同上
echo gun is not unix | grep -b -o "not" #打印样式匹配所位于的字符或字节偏移：?
grep -l "text" file1 file2 file3...
grep -l "text" ncbi #搜索多个文件并查找匹配文本在哪些文件中
cd ncbi/
grep -l "d" lll.txt  k.txt 
grep "d" -r -n #在多级目录中对文本进行递归搜索
echo "hello world" | grep -i "HELLO" #忽略匹配样式中的字符大小写
grep -q "z" nex.txt #静默输出
seq 1 1000|grep '^1' #匹配以1开头的行
seq 1 1000|grep '[24680$]' #匹配包含2or4or6or8or0的行
seq 1 1000|grep -E -w '0|16' #显示包含0或16的列 只显示全字符合的列
grep -w 完全匹配

```

