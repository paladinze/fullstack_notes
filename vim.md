# Vim: the UNIX editor

## reference
- https://www.fprintf.net/vimCheatSheet.html

1. Two modes: command mode and insert mode (controlled by Esc and i keys)

2. delete:command mode: d; insert mode: backspace

3. moving by search: /word_being_searched

4. closing and saving: 
	1.ZZ		write and quit
	2.:w		write
	3.:w!		force write
	3.:q!		discard changes and quit file
	
5.Set Vim Preferences:
	1.:set ic (ignore cases when search)
	2.:set ws (enable wrap scan)
	3.:set nu (display line number)
	4.:set paste (correct formating for paste)
	
6.Replace keyword:
	1.:%s/Ze/goodZe/gc (global replace with prompt)	
	
7.Moving text paragraph
	1.press v at the start point => move the cursor to end point
	2.press d (delete the text)
	3.press p (paste the text)

8.Sorting lines (alphabetical/numerical)
	1.press v at the start point => move the cursor to end point
	2.type !sort -n

9.Split screen edit
	1.vim file_1
	2.:sp file_2
	3.ctrl + ww (switch screen)

10.Navigate though cpp procedures
	1.ctags *.cpp
	2.vim -t print_foo (navigate to procedure)
	3.inside the file: position the cursor at the beginning of the identifier and press Ctrl+] 
	
11.Drawing Comment box
	1.edit ~/.vimrc  => add the following two lines
	2.:ab #b /************************************************    
	3.:ab #e ************************************************/
	
12.Other useful setting to put in ~/.exrc : 
	:set autoindent
	:set autowrite
	:ab #d #define
	:ab #i #include
	:ab #b /************************************************
	:ab #e ************************************************/
	:ab #l /*----------------------------------------------*/
	:set sw=4

13.Read command file
	1.man sort | ul -i | vim -  (ul -i will convert escape chars to readable format)

14.remove write protection
	1.:shell
	2.chmod u+w file.txt
	3.exit
	4.:w!

15.edit all files containing a given word
	1.vim `fgrep -l indentation_level *.c`
	
16.switching position
	1.in file: Cheng, Ze => Ze, Cheng
	2.:%s/\([^,]*\), \(.*$\)/\2, \1/

