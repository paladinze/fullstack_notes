## Ascii、GBK、UTF、Unicode
* Ascii（1个字节）
* GBK是国内的编码标准（2个字节）
* Unicode是国际编码标准（2个字节）
* UTF是Unicode实现的另一个标准
* UTF-8就是每次8个位传输数据： 联网上使用最广的一种unicode的实现方式
* UTF-8最大的一个特点，就是它是一种变长的编码方式。
  * 它可以使用1~4个字节表示一个符号，根据不同的符号而变化字节长度，当字符在ASCII码的范围时，就用一个字节表示，保留了ASCII字符一个字节的编码做为它的一部分，注意的是unicode一个中文字符占2个字节，而UTF-8一个中文字符占3个字节）。
* 从unicode到utf-8并不是直接的对应，而是要过一些算法和规则来转换。