在Java中,String类包含有50多个方法来实现字符串的各种操作,以下介绍一些我们需要经常使用的方法.

### (1)字符串的连接

public String concat(String str) 

该方法的参数为一个String类对象,作用是将参数中的字符串str连接到原来字符串的后面. 

### (2)求字符串的长度

public int length()

返回字串的长度,这里的长度指的是字符串中Unicode字符的数目.

### (3)求字符串中某一位置的字符

public char charAt(int index)

该方法在一个特定的位置索引一个字符串,以得到字符串中指定位置的字符.值得注意的是,在字符串中第一个字符的索引是0,第二个字符的索引是1,依次类推,最后一个字符的索引是length()-1. 

### (4)字符串的比较

比较字符串可以利用String类提供的下列方法:

**1)public int compareTo(String anotherString)**

该方法比较两个字符串,和Character类提供的compareTo方法相似,Character类提供的compareTo方法比较的是两个字符类数据,而这里比较的是字符串数据.

其比较过程实际上是两个字符串中相同位置上的字符按Unicode中排列顺序逐个比较的结果.如果在整个比较过程中,没有发现任何不同的地方,则表明两个字符串是完全相等的,compareTo方法返回0;如果在比较过程中,发现了不同的地方,则比较过程会停下来,这时一定是两个字符串在某个位置上不相同,如果当前字符串在这个位置上的字符大于参数中的这个位置上的字符,compareTo方法返回一个大于0的整数,否则返回一个小于0的整数. 

**2)public boolean equals(Object anObject)**

该方法比较两个字符串,和Character类提供的equals方法相似,因为它们都是重载Object类的方法.该方法比较当前字符串和参数字符串,在两个字符串相等的时候返回true,否则返回false. 

**3)public boolean equalsIgnoreCase(String anotherString)**

该方法和equals方法相似,不同的地方在于,equalsIgnoreCase方法将忽略字母大小写的区别.

### (5)从字符串中提取子串

利用String类提供的substring方法可以从一个大的字符串中提取一个子串,该方法有两种常用的形式:

**1)public String substring(int beginIndex)**

该方法从beginIndex位置起,从当前字符串中取出剩余的字符作为一个新的字符串返回.

**2)public String substring(int beginIndex, int endIndex)**

该方法从当前字符串中取出一个子串,该子串从beginIndex位置起至endIndex-1为结束.子串返的长度为endIndex-beginIndex. 

### (6)判断字符串的前缀和后缀

判断字符串的前缀是否为指定的字符串利用String类提供的下列方法:

**1)public boolean startsWith(String prefix)**

该方法用于判断当前字符串的前缀是否和参数中指定的字符串prefix一致,如果是,返回true,否则返回false.

**2)public boolean startsWith(String prefix, int toffset)**

该方法用于判断当前字符串从toffset位置开始的子串的前缀是否和参数中指定的字符串prefix一致,如果是,返回true,否则返回false.

判断字符串的后缀是否为指定的字符串利用String类提供的方法:

**public boolean endsWith(String suffix)**

该方法用于判断当前字符串的后缀是否和参数中指定的字符串suffix一致,如果是,返回true,否则返回false.

### (7)字符串中单个字符的查找

字符串中单个字符的查找可以利用String类提供的下列方法:

**1)public int indexOf(int ch)**

该方法用于查找当前字符串中某一个特定字符ch出现的位置.该方法从头向后查找,如果在字符串中找到字符ch,则返回字符ch在字符串中第一次出现的位置;如果在整个字符串中没有找到字符ch,则返回-1. 

**2)public int indexOf(int ch, int fromIndex)**

该方法和第一种方法类似,不同的地方在于,该方法从fromIndex位置向后查找,返回的仍然是字符ch在字符串第一次出现的位置. 

**3)public int lastIndexOf(int ch)**

该方法和第一种方法类似,不同的地方在于,该方法从字符串的末尾位置向前查找,返回的仍然是字符ch在字符串第一次出现的位置.

**4)public int lastIndexOf(int ch, int fromIndex)**

该方法和第二种方法类似,不同的地方在于,该方法从fromIndex位置向前查找,返回的仍然是字符ch在字符串第一次出现的位置.

### (8)字符串中子串的查找

字符串中子串的查找与字符串中单个字符的查找十分相似,可以利用String类提供的下列方法:

**1)public int indexOf(String str)**

**2)public int indexOf(String str, int fromIndex)**

**3)public int lastIndexOf(String str)**

**4)public int lastIndexOf(String str, int fromIndex)** 

### (9)字符串中字符大小写的转换

字符串中字符大小写的转换,可以利用String类提供的下列方法:

**1)public String toLowerCase()**

该方法将字符串中所有字符转换成小写,并返回转换后的新串.

**2)public String toUpperCase()**

该方法将字符串中所有字符转换成大写,并返回转换后的新串. 

### (10)字符串中多余空格的去除

**public String trim()**

该方法只是去掉开头和结尾的空格,并返回得到的新字符串.值得注意的是,在原来字符串中间的空格并不去掉. 

### (11)字符串中字符的替换

**1)public String replace(char oldChar,char newChar)**

该方法用字符newChar替换当前字符串中所有的字符oldChar,并返回一个新的字符串.

**2)public String replaceFirst(String regex, String replacement)**

该方法用字符串replacement的内容替换当前字符串中遇到的第一个和字符串regex相一致的子串,并将产生的新字符串返回. 

**3)public String replaceAll(String regex, String replacement)**

该方法用字符串replacement的内容替换当前字符串中遇到的所有和字符串regex相一致的子串,并将产生的新字符串返回. 

 

1.**字符串变量与StringBuffer类** 

创建StringBuffer类对象

StringBuffer类对象表示的是字符串变量,每一个StringBuffer类对象都是可以扩充和修改的字符串变量.以下是常用的StringBuffer类构造函数:

**(1)public StringBuffer()**

**(2)public StringBuffer(int length)** 

**(3)public StringBuffer(String str)** 

###  (12)分割函数 split 的用法

参考 https://www.cnblogs.com/ggjucheng/p/3352419.html

