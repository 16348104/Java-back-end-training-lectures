# 补1. 正则表达式 `Regular Expression`

> RegEx = Regular Expression

1. 括号 `Brackets`
    - [abc]	
    - [^abc]	
    - [0-9]	
    - [^0-9]	
    - (x|y)	 
    - `[a-d[m-p]]`	a 到 d 或 m 到 p：[a-dm-p]（并集）
    - `[a-z&&[def]]`	d、e 或 f（交集）
    - `[a-z&&[^bc]]`	a 到 z，除了 b 和 c：[ad-z]（减去）
    - `[a-z&&[^m-p]]`	a 到 z，而非 m 到 p：[a-lq-z]（减去）           
    
2. 元字符 `Metacharacters`    
    - .	
    - \w	
    - \W	
    - \d
    - \D
    - \s
    - \S
    - \b
    - \B
    - \0
    - \n
    - \f
    - \r
    - \t
    - \v
    - \xxx
    - \xdd
    - \uxxxx

3. POSIX 字符类（仅 US-ASCII）    
    - `\p{Lower}`	小写字母字符：[a-z]3. 量词 `Quantifiers`    
    - `\p{Upper}`	大写字母字符：[A-Z]    - n+	
    - `\p{ASCII}`	所有 ASCII：[\x00-\x7F]    - n*	
    - `\p{Alpha}`	字母字符：[\p{Lower}\p{Upper}]    - n?	
    - `\p{Digit}`	十进制数字：[0-9]    - n{X}	
    - `\p{Alnum}`	字母数字字符：[\p{Alpha}\p{Digit}]    - n{X,Y}	
    - `\p{Punct}`	标点符号：!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~    - n{X,}	
    - `\p{Graph}`	可见字符：[\p{Alnum}\p{Punct}]    - n$	
    - `\p{Print}`	可打印字符：[\p{Graph}\x20]    - ^n	
    - `\p{Blank}`	空格或制表符：[ \t]    - ?=n	
    - `\p{Cntrl}`	控制字符：[\x00-\x1F\x7F]    - ?!n	
    - `\p{XDigit}`	十六进制数字：[0-9a-fA-F]    
    - `\p{Space}`	空白字符：[ \t\n\x0B\f\r]

4. 量词 `Quantifiers`    
    - n+	
    - n*	
    - n?	
    - n{X}	
    - n{X,Y}	
    - n{X,}	
    - n$	
    - ^n	
    - ?=n	
    - ?!n	
    
5. `java.util.regex`

    - Pattern
        - compile
        - split
    - Matcher
        - find
        - group                    
    
    
    