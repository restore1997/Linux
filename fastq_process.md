fastq处理笔记

```{shell}
less -S SRR1039510_1.fastq #单行查看SRR1039510_1.fastq文件
less -S SRR1039510_1.fastq|paste - - -|cut -f 1|wc #统计文件中一共有多少条序列信息
less -S SRR1039510_1.fastq|grep ^@ |wc #统计文件中一共有多少条序列信息
less -S SRR1039510_1.fastq|grep ^@|awk '{print}' #输出所有的SRR1039510_1.fastq文件中的标识符(即以@开头的那一行)
less -S SRR1039510_1.fastq|grep ^@ -A 1 #输出所有的SRR1039510_1.fastq文件中的标识符和序列信息（第一、二行）
awk  '/^@/{getline; print}' SRR1039510_1.fastq #输出所有的SRR1039510_1.fastq文件中的序列信息（第二行）
less -S SRR1039510_1.fastq|grep ^+ #输出第三行
sed -n '4~4p' SRR1039510_1.fastq #输出质量值信息(即每个序列的第四行)
less SRR1039510_1.fastq|paste - - - - |cut -f 2|grep -i -o [ATCGN]|wc #统计文件中SRR1039510_1.fastq文件里面的序列的碱基总数
less SRR1039510_1.fastq|paste - - - -|cut -f 2 |awk '{sum+=length($0)} END {print sum}' #同上
less -S SRR1039510_1.fastq|paste - - - - |cut -f 2|grep -o ^[ATCGN]|sort|uniq -c # 统计reads_1.fq 中所有序列的第一位碱基的ATCGN分布情况(ATCGN分别个数)(uniq)
less -S SRR1039510_1.fasta|awk '{if($0~/^>/)print $0;else print substr($0,6,length($0)-10)}'|less -S #删除SRR1039510_1.fasta文件每条序列的前后五个碱基
less -S reads_1.fq|paste - - - -|cut -f1,2|tr "\t" "\n"|tr "@" ">" >read_1.fa # 将reads_1.fq 转为reads_1.fa文件(即将fastq转化为fasta)(tr)
```

