# Regular Expressions

2.Substitute pattern: s/ab*c/def/;

3.Matching single character:
	1.[a-zA-Z0-9_]  # match any single letter in the brackets
	2.[^aeiouAEIOU] # match any single letter not in the brackets

4.Matching Multiple Characters:
	1. (+):match 1 or more times
	2. (?):match 0 or 1 times; non-greedy match
	3. (*):match 0 or more times; greedy match
	4. (.):any character except newline
	5. (^):beginning of string
	6. ($):end of string
	7. (|):alternate
	8. (\s): any whitespace character
	9. (\d): any digital character
	10. (\w): any word character
	
	11. exact number matching needed:
		1.x{m,}: m or more X
		2.x{m}: m X
		3.x{m,n}: m to n X
	
	
