一、在任意文件夹下面创建形如 1/2/3/4/5/6/7/8/9 格式的文件夹系列。
```{shell}
mkdir -p 1/2/3/4/5/6/7/8/9 # -p 用于多个操作
```
二、在创建好的文件夹下面，比如我的是/Users/jimmy/tmp/1/2/3/4/5/6/7/8/9 ，里面创建文本文件 me.txt
```{shell}
cd 1/2/3/4/5/6/7/8/9/；touch me.txt #   分号；可以在同一行写两条命令，与R相同
```
三、在文本文件 me.txt 里面输入内容:
> Go to: http://www.biotrainee.com/
>
> I love bioinfomatics.
>
> And you ?

```{shell}
vim me.txt # i 编辑   ； Esc ： w q 保存并退出
# 或者
cat > me.txt
```
四、删除上面创建的文件夹 1/2/3/4/5/6/7/8/9 及文本文件 me.txt
```{shell}
rm -r 1 # #递归删除 将指定目录下的所有文件与子目录一并处理 很危险
```
五、在任意文件夹下面创建 folder1~5这5个文件夹，然后每个文件夹下面继续创建 folder1~5这5个文件夹，效果如下
```{shell}
mkdir -p folder{1..5}/folder{1..5} #思想很重要
```
六、在第五题创建的每一个文件夹下面都 创建第二题文本文件 me.txt ，内容也要一样。(这个题目难度超纲，讲义一个月后再回过头来做)
```{shell}
# 参考小洁姐习题答案
for dirs in folder{1..5}/folder{1..5}; do  cp me.txt $dirs; done
# 或者
echo folder{1..5}/folder{1..5} | xargs -n 1 cp -v me.txt
```
七，再次删除掉前面几个步骤建立的文件夹及文件
```{shell}
rm -r folder{1..5}
# 或者
rm -r folder* # *是正则表达式 用于匹配 匹配之前的项0次或者多次
```
八、下载 `http://www.biotrainee.com/jmzeng/igv/test.bed` 文件，后在里面选择含有 `H3K4me3` 的那一行是第几行，该文件总共有几行。
```{shell}
wget http://www.biotrainee.com/jmzeng/igv/test.bed # wget用来从指定的URL下载文件 非常稳定 适应性强
grep -n "H3K4me3" test.bed # -n 显示行数
less -S test.bed |wc -l # wc -l 显示行数
```
九、下载 `http://www.biotrainee.com/jmzeng/rmDuplicate.zip` 文件，并且解压，查看里面的文件夹结构
```{shell}
wget http://www.biotrainee.com/jmzeng/rmDuplicate.zip 
unzip rmDuplicate.zip # unzip解压zip文件 gunzip解压gz文件 
tree rmDuplicate #查看目录结构
```
十、打开第九题解压的文件，进入 `rmDuplicate/samtools/single` 文件夹里面，查看后缀为 `.sam` 的文件，搞清楚 生物信息学里面的`SAM/BAM` 定义是什么。
```{shell}
cd rmDuplicate/samtools/single
less -S *.sam
# SAM是一种基于文本的格式，用于存储对齐到参考序列的生物序列。它广泛用于存储由二代测序技术生成的数据，如核苷酸序列。
# BAM文件是SAM文件的二进制等效文件，它以压缩的二进制表示形式存储相同的数据。
```
十一、安装 `samtools` 软件
```{shell}
conda search samtools #使用conda软件 搜索 （需提前安装miniconda）
conda install -y santools #安装
ls -t
```
十二、打开 后缀为`BAM` 的文件，找到产生该文件的命令。 提示一下命令是：
```
/home/jianmingzeng/biosoft/bowtie/bowtie2-2.2.9/bowtie2-align-s --wrapper basic-0 -p 20 -x /home/jianmingzeng/reference/index/bowtie/hg38 -S /home/jianmingzeng/data/public/allMouse/alignment/WT_rep2_Input.sam -U /tmp/41440.unp
```

```{shell}
# 没看懂上面的提示命令是干啥的..
less -S *.sam  #实际上sam文件只有一个 不匹配也行
less readme.txt #在readme.txt里找到了它 ，如下
# cat tmp.header tmp.sam |samtools view -bS - |samtools sort - -o tmp.sorted.bam
```



十三题、根据上面的命令，找到我使用的参考基因组 `/home/jianmingzeng/reference/index/bowtie/hg38`具体有多少条染色体。
```{shell}
# Permission denied 没有权限访问
```
十四题、上面的后缀为`BAM` 的文件的第二列，只有 0 和 16 两个数字，用 `cut/sort/uniq`等命令统计它们的个数。
```{shell}
# 此处应该是SAM文件的第二列
less -S tmp.sam |cut -f 2| grep 0|wc -l #29  管道符 
less -S tmp.sam |cut -f 2| grep 16|wc -l #24
less -S tmp.sam |cut -f 2|wc -l #53 加起来刚刚好
```
十五题、重新打开 `rmDuplicate/samtools/paired` 文件夹下面的后缀为`BAM` 的文件，再次查看第二列，并且统计
```{shell}
# 第二列并非简单的0和16两个数，所以需要cut/sort/uniq
cut -f 2 tmp.sam |sort |uniq -c #先排序 再uniq并输出重复数量
```
十六题、下载 `http://www.biotrainee.com/jmzeng/sickle/sickle-results.zip` 文件，并且解压，查看里面的文件夹结构， 这个文件有2.3M，注意留心下载时间及下载速度。
```{shell}
wget http://www.biotrainee.com/jmzeng/sickle/sickle-results.zip
unzip sickle-results.zip
cd sickle-results/ ； tree
```
十七题、解压 `sickle-results/single_tmp_fastqc.zip` 文件，并且进入解压后的文件夹，找到 `fastqc_data.txt` 文件，并且搜索该文本文件以 `>>`开头的有多少行？
```{shell}
unzip single_tmp_fastqc.zip #常规操作
cd single_tmp_fastqc/
less -S fastqc_data.txt
less -S fastqc_data.txt|grep ^">>"|wc -l #注意区分 > 和 <
```
十八题、下载 `http://www.biotrainee.com/jmzeng/tmp/hg38.tss` 文件，去NCBI找到`TP53/BRCA1`等自己感兴趣的基因对应的 `refseq数据库` ID，然后找到它们的`hg38.tss` 文件的哪一行。
[https://www.ncbi.nlm.nih.gov/gene/7157](https://www.ncbi.nlm.nih.gov/gene/7157)

```{shell}
wget http://www.biotrainee.com/jmzeng/tmp/hg38.tss
less -S hg38.tss #看一下里面的结构
less -S hg38.tss|grep -n NR_027676 #进入NCBI网站 找到TP53对应的ID为NR_027676 grep一下
less -S hg38.tss|grep -n NM_001126112 #BRCA1对应的ID是不同的形式
# 这一题应该再写一篇文章
```
十九题、解析`hg38.tss` 文件，统计每条染色体的基因个数。
```{shell}
cut -f 2 hg38.tss |sort |uniq -c #同上 这个也该好好另分析一下
```
二十题、解析`hg38.tss` 文件，统计`NM`和`NR`开头的熟练，了解`NM`和`NR`开头的含义。
```{shell}
less -S hg38.tss
```

![1554558186157](盘一盘 生信人的Linux考试.assets/1554558186157.png)

参考来源：生信技能树&&Linux命令大全