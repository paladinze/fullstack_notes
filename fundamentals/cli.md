# Unix

## file navigation
- Remove file
	- remove a file: `rm -f`
	- remove direcotry: `rm -rf`
	- remove everything: `rm -rf *`

- List file
	- list files: `ls`
	- ordered list: `ls -lrt`
	- show hidden files: `ls -a`
	
- find and delete file
	- find ./ -name "*.js" -type f -delete

## compression
- compress file 
	- tar -cvzf filename.tar.gz filename/ (tar.gz)

- decompress file
	- tar -xvzf filename.tar.gz (tar.gz or tgz)
	- tar -xvjf filename.tar.bz2 (bzip2)
	- zcat filename.tar.Z | tar xf - (Z or Huffman coding)
	

## search
5.Searching Keywords:
	1.grep (when special character are part of the keyword)
		1.grep keyword file_name 
		2.grep -i "keyword" file_name (case insensitive)
		
	2.egrep (when want to use metachracters, such as +, ? , |
		1.egrep "keyword_1|keyword_2" filename
	
6.Searching Files:
	1.find -name file_name (search the system for file_name and return the path)

7.Show Current Paths: 
	1.pwd
	
8.show file size:
	1.du -sh file_name

9.show disk usages:
	1.df -h full_path
	
10.create empty file or directory:
	1.touch filename
	2.mkdir -p (create all required path)

11.setting alias:	
	1.alias command 'regular command'
	2.modify .cshrc to enable alias when open the shell
	
12.show history of commands:
	1.history
	
13.show current shell
	1.ps -p $$

14.discard standard error
	1.find / -name core 2> /dev/null (stdin = 0, stdout = 1, stderr = 2)

15.issue two commands in sequence
	1.lpr /tmp/t2 && rm /tmp/t2
	
16.issue the second command only if the first failed
	1.cp --preserve --recursive /etc/* /spare/backup \
		|| echo "Did NOT make backup"
	
17.show current os info 
	1.uname -a

18.send email
	1.text: diff file1 file2 | mailx cheng
	2.file: uuencode file1 file1 | mailx cheng

19.Sort text file 
	1.sort -n -k 4 (numercial sort on column 4)
	
20.extract from string and parse
	1. echo "Ze Cheng" | awk '{print $1}' | xargs $1

21.remote file copying
	1.Method1:
		1.ftp <hostname>
		2.ftp> get <absolute host path> <destination path>
	2.Method2:
		1.scp 'svvgar-nx21:/proj/ipcad-tier2-test2/cheng/main/pd/tiles/svdc_backup/*.tar.gz' .
22.check digital footprint
	1.md5sum file

24.date formatting
	1.date +'%d/%m/%y'
	
25.check current hostname
	1.hostname
		
26.check search path
	1.echo $PATH

27.create your own commands
	1.cd /usr/local/bin
	2.create the shell script and add execution permission

		
		
		
	

