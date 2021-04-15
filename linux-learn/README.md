#linux shell常用命令

@文件管理类：
1.cat：连接文件并打印到标准输出设备上。实现文件内容的查看
具体命令：cat 文件     ----查看文件
	  cat > 文件   ----创建文件（不能编辑文件）
	  cat file1 file2 > file3 -----将几个文件合并成一个（你可以尝试一下把file3的名字换成file2然后回车～～～～）

2.chmod：控制用户权限（owner，group，others）,查看文件现有权限的命令：ls -l。只有文件所有者和超级用户可以修改文件或者目录的权限。权限主要分为R，W，X（读，写，执行），对应数字为4，2，1。
具体命令：chmod [-cfvR] [--help] [--version] mode file
          chmod ugo+r filename -----将filename文件权限设置为所有人可读
	  chmod a+r filename -----将filename文件设置为所有人可读
	  chmod ug+w,o-w file1 file2 ----将file1和2设置为档案拥有者与其所属同一个群体可以写入，但其他以外的人不可以写入
	  chmod 777 file（chmod a=rwx file） ----文件所有权限可以使用

3.diff：以逐行的方式比较文件差异。若制定比较目录，则会比较目录中相同名字的文件，但不会比较其子目录
具体命令：diff file1 file2----比较两个文件差异
	  diff file1 file2 -y ---并排显示差异



