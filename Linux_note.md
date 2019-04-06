```{shell}
# ps命令用于报告当前系统的进程状态。可以搭配kill指令随时中断、删除不必要的程序。
ps -ef|grep userid #显示有关userid的进程
# help查看帮助文档
help shopt #查看shopt的帮助文档
help -s shopt#简单显示
#vim 删除整行命令
dd

### 文件目录操作
# mkdir -p建立多层|多个目录
mkdir -p test1 test2 test3 #多个
mkdir -p test1/test2/test3/ #多层
#cd cd命令用来切换工作目录至dirname
cd / #进入根目录
cd    #进入用户主目录；
cd ~  #进入用户主目录；
cd -  #返回进入此目录之前所在的目录；
cd ..  #返回上级目录（若当前目录为“/“，则执行完后还在“/"；".."为上级目录的意思）；
cd ../..  #返回上两级目录；
cd !$  #把上个命令的参数作为cd参数使用。
# ls 目录展示
ls -l #显示长的完整信息
ls -a #显示隐藏文件(all)
ls -tr #按修改时间反向排序
ls -lh #查看文本大小，以人可读的方式
ls *gz # *是通配符 常用ls *gz|
ls -l -tr #可以合用
# touch创建文本
touch new.txt
touch del{1..10}.txt # 创建10个文本
# rm 文件|目录删除
rm -i #删除前询问 y enter
rm -r #递归删除 将指定目录下的所有文件与子目录一并处理 很危险
rm -f #强制删除
rm ./link1 #软链失效：删除软链
rm file1 file2 #删除文本
rm *.sam #批量删除
rm -r test/ #删除路径
# cp 文本/目录复制 cp [参数] 源文件 目标文件 ；需要两个路径 若不带路径，默认./  ；cp默认会覆盖同名文本；到另一个文件夹的前提是目标文件夹路径存在
cp -i #覆盖前询问
cp -r #复制目录及目录内的所有项目
cp -f #强制覆盖
cp readme.txt ncbi
cp -r public/sra/ hhh#把public下的sra目录复制到hhh目录下
# less 查看文本 eg： less [参数] 目标文件;最常用来查看文本，特别是大文本 不能编辑/改变原文本，只能重定向
less -S #单行显示
less -N #行号加入编号
less -N nex.txt 
# vim 编辑文本 ；不能来操作大文本；文本不存在时保存成新文本；不能用来编辑目录
vim nex.txt #编辑nex.txt
i #insert状态
：wq #先按ESC 写入，退出
：q！ #不保存退出
# cat 输出/入文本 eg： cat [参数] 文本
cat -n #按行数编号
cat -A #等价于vET 显示不可打印字符，行尾显示“$”；
cat dddd.txt -n 
zcat sample1.fq.gz# 显示压缩包 指定要显示其中文件内容的压缩包
# head 从头展示文件行数 eg： head [参数] 文本
head -n num #展示文本前num行
head -n 3 ~/.bashrc
head -n 5 SRR_Acc_List.txt
# tail从尾展示文件行数
tail -n num #展示文本后num行
cat ~/.bashrc|tail -n 3
tail -n 3 dddd.txt
cat dddd.txt |tail -n 3
# more 查看文本 ；回车键逐行往下翻(无法再往上翻)；空格键直接翻下一页；q退出
more his_20190317.txt
# tree 树形展示
tree -d ；只显示目录
tree -L num ；显示num层目录
tree -d
tree -L 2
# mv 文件/目录 移动|更名 eg： mv [参数] 目录1 目录2
#移动：mv 目录1/ 目录2
#更名：mv 目录1 目录2 ;mv 文本1 文本2
mv SRR_Acc_List.txt /ncbi
cd
mv SRR_Acc_List.txt /trainee/vip15/ncbi/
ls
cd ncbi/
mv SRR_Acc_List.txt lll.txt
# > 重定向 ；重定向意味着清空文件，重新输入
cat ~/.bashrc > ~/.bashrcbk
cat lll.txt >k.txt 把lll.txt内容赋值给k.txt（原有k.txt内容删除）
# >> 追加
echo alias ll="ls -l" >> ~/.bashrcbk
echo lll.txt >>oo.txt 在oo.txt后面输入（追加）“lll.txt”
# | 管道符
less ~/.profile | grep '#'
# history 查看历史命令
history |tail -n 10 #例子：查看后十行记录
history |tail -n 5|less -S #查看后五行记录并传给less
history > history1.txt #重定向history内容保存起来
history|tail -n 5 >> history1.txt #追加后五行到之前文本里
# ln 建立链接 eg： ln [参数] [目录1/文本1] [目录2/文本2]
ln -s ~qmcui/.bashrc ~/ #建立软链接
ln -s ~  qmcui/.bashrc ~/.bashrc_bk #建立软连接并更名
# wget -c ftp下载
wget -c link
#which CMD 查看命令路径
which CMD
#ps -ef |grep userID 查看任务
ps -ef |grep userID
#top -c 查看任务是否在内存中运行
top -c
#kill PID 杀掉任务
kill PID

### 压缩解压命令
# gzip压缩文本 gunzip解压文本 ；压缩成功会默认删掉源文件
gzip nex.txt # 压缩nex.txt文件
gunzip nex.txt.gz；ls -tr #解压nex.txt.gz文件
gzip -c nex.txt > nex.txt.gz #保留源文件，并新生成压缩文件
unzip rmDuplicate.zip #解压zip文件
# tar 最常用的打包命令
tar -cvf new.tar *.txt # 打包
tar -xvf old.tar # 拆tar包
tar -zcvf new.tar.gz ./# 打包和gzip压缩
tar -zxvf old.tar.gz # 解压打包
tar -jcvf new.tar.bz2 *.jpg # 打包和bzip2压缩
tar -jxvf old.tar.bz2 # bunzip2解压打包
tar -cvf new.tar *.txt；ls
tar -xvf new.tar；ls
tar -zcvf new.tar.gz *.txt；ls
#解压例子：
tar -xZf all.tar.Z # **
unzip all.zi# **
bunzip2 all.bz2
uncompress all.Z

### 进阶命令一
# cut 文件切割命令eg： cut [参数] 文本/管道符内容参数：
cut -d：自定义分隔符 ,默认为制表符\t
cut -f：分割符分割文本后，指定输出第几列
who | cut -d " " -f 1 #分割who文本后，输出第一列
echo $PATH |cut -d ":" -f 1
cut ss.txt -d "0" -f 1 > lll.txt #用“0”分割ss.txt文本后,输出第一列到lll.txt文本
cut -d "0" -f 1 complement ss.txt >lll.txt# 向lll.txt输出除第一列之外的ss.txt分割文本
cut ss.txt -d "0" -f 2-4 > lll.txt #输出第2到4列
echo $PATH |cut -d ":" -f 1 #显示以“：”分割的第一列的环境变量
echo $PATH #显示环境变量
#/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin
PATH=$PATH:/home/tito/bin #添加/home/tito/bin到PATH环境变量
echo $PATH
#/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/tito/bin
# paste 按列操作文本 用于将多个文件按照列队列进行合并 eg： paste [参数] 文本/管道符内容
paste -d #指定分隔符
paste -s #将每个文件合并成行而不是按列粘贴
zcat SRR1039510_1.fastq.gz  | paste - - - - |less -S #按列查看解压SRR1039510_1.fastq.gz之后的内容
paste nex.txt readme.txt > dddd.txt
paste -d ":" nex.txt readme.txt
paste -s nex.txt readme.txt
# sort 排序
sort -t #指定分隔符
sort -k #指定区域
sort -n #按照数值大小进行排序
sort -r #相反的顺序排序
cut -f 1,3,4,5 
Homo_sapiens.GRCh38_MT.79.gtf | grep  -v '#!' > tmp
sort -r -n -k 3 tmp
# uniq 去除文件中的重复行 sort|uniq 组合使用
uniq -c #显示每行连续出现的次数
uniq -d #仅显示重复出现的行
uniq -u #仅显示没有连续出现的行
cut -f 2 Homo_sapiens.GRCh38_MT.79.gtf | sort|uniq -c
# find 寻找 eg： find [参数] 目录/文本
find -name "*.gz" #寻找.gz结尾的文件
find -size +500M #寻找大于500M的文件
find -size -1M #寻找小于1M的文件
# tr 转换或删除文件中的字符 eg：  tr [参数] 文本
tr -s #缩减连续重复的字符成指定的单个字符
tr -d #删除
cat testfile |tr a-z A-Z # 小写变大写
echo $PATH | tr ":" "\n" |less -S   # 替换\t为换行cat file | tr -s "\n" > new_file  # 删除空行
sed -i '1d' k.txt  #删除第一行
sed -i 'nd' filename #删除第n行
sed -i '$d' filename #删除最后一行
# wc 行数/字符/文本大小计数 eg： wc [参数] 文本/管道符内容
wc -l #计算行数
wc k.txt # 19  19 208   k.txt有19行 19个字符 208chars|bytes
# bc 数学运算
bc #进入数学运算
scale=5 #保留小数点后5位
quit #退出
# jobs 显示Linux中的任务列表及任务状态，包括后台运行的任务。
find -name password &
jobs -l #[1]+  6717 Done                    find -name password
        #输出信息的第一列表示任务编号，第二列表示任务所对应的进程号，第三列表示任务的运行状态，第四列表示启动任务的命令。
jobs -l：显示进程号；
jobs -p：仅任务对应的显示进程号；
jobs -n：显示任务状态的变化；
jobs -r：仅输出运行状态（running）的任务；
jobs -s：仅输出停止状态（stoped）的任务。
# bg 将作业放到后台运行，使前台可以执行其他任务。
bg 1   #后台执行任务号为1的任务 如果系统中只有一个挂起的任务时,即使不为该命令设置参数"1"，也可以实现这个功能。
find / -name password &     #后台执行任务 任务后面加&，与bg效果相同
# fg 命令用于将后台作业（在后台运行的或者在后台挂起的作业）放到前台终端运行。
fg 1
# nohup命令可以将程序以忽略挂起信号的方式运行起来，被运行的程序的输出信息将不会显示到终端。
nohup command > myout.file 2>&1 &
# pwd命令以绝对路径的方式显示用户当前工作目录。
pwd #/trainee/vip15
# df命令用于显示磁盘分区上的可使用的磁盘空间。默认显示单位为KB。
# du命令也是查看使用空间的，但是与df命令不同的是Linux du命令是对文件和目录磁盘使用的空间的查看，还是和df命令有一些区别的。
# top命令可以实时动态地查看系统的整体运行情况，是一个综合了多方信息监测系统性能和运行信息的实用工具。
# free命令可以显示当前系统未使用的和已使用的内存数目，还可以显示被内核使用的内存缓冲区。
# netstat命令用来打印Linux中网络系统的状态信息，可让你得知整个Linux系统的网络情况。
# ssh命令是openssh套件中的客户端连接工具，可以给予ssh加密协议实现安全的远程登录服务器。
# scp命令用于在Linux下进行远程拷贝文件的命令，和它类似的命令有cp，不过cp只是在本机进行拷贝不能跨服务器，而且scp传输是加密的。可能会稍微影响一下速度。当你服务器硬盘变为只读read only system时，用scp可以帮你把文件移出来。
# diff命令在最简单的情况下，比较给定的两个文件的不同。如果使用“-”代替“文件”参数，则要比较的内容将来自标准输入。
# chown命令改变某个文件或目录的所有者和所属的组
# chgrp命令用来改变文件或目录所属的用户组。
# groups命令在标准输入输出上输出指定用户所在组的组成员
# echo命令用于在shell中打印shell变量的值，或者直接输出指定的字符串。
echo -e #激活转义字符
shift g #显示最后一行


### conda 
# 安装R包 
conda search biocondutor -deseq2
conda install bioconductor-deseq2 #conda会自动安装最新版本的deseq2以及对应版本的R，以及各种依赖的其他R包。
```

