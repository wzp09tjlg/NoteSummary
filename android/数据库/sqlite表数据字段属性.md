在使用sqlite数据库肯定会创建表，表中各个属性的字段在sqlite中支持哪些属性，这个需要注意下，和其他的数据引擎不一样，在sqlite中虽然采用的是动态数据类型，数据库引擎会根据数据的类型进行判断，但是为了更好的维护数据和对版本迭代，在创建表结构时 数据类型的工作是必不可少的。sqlite具有以下数据类型：
NULL 空值
INTEGER 带符号的整型，具体取决于存入数字的范围大小
REAL 浮点数字，存储为8-byte IEEE浮点数
TEXT 字符串文本
BLOB 二进制对象

sqlite3还支持以下数据类型：
smallint 16位元的整数型
integer  32位元的整数
decimal(p,s) p精确至和s大小的十进位整数,精确值p是指全部由几个数(digits)大小值，s是指小数点后有几位数,如果没有特别支出那么系统会设定p=5,s=0
float 32位元的实数
double 64位元的实数
char(n) n长度的字符串 n不能大于254
varchar(n) 长度不固定，其最大长度是n，n最大不超过4000；
text 长度可变的飞Uniicode数据，大小是2^31 - 1个字符（2147483647）
graphic(n) 和 char(n) 一样，不过其单位是两个字元的double-bytes, n不能超过127，这个形态是为了支援两个字元的长度的字体，例如中文字
vargraphic(n)可变长度且其最大长度为n的双元字串，n不能超过2000
date 包含年份 月份 日期
time 包含小时 分钟 秒
timestamp 包含年 月 日 时 分 秒 千分之一秒
datetime 包含日期时间格式 必须写成‘2016-10-09’ 不能写成‘2016-10-9’否则会在读取时产生错误。

举个栗子，创建一张表 格式如下：
    CREATE TABLE IF NOT EXISTS ex2(    
    a VARCHAR(10),    
    b NVARCHAR(15),   
    c TEXT,    
    d INTEGER,   
    e FLOAT,   
    f BOOLEAN,    
    g CLOB,    
    h BLOB,    
    i TIMESTAMP,   
    j NUMERIC(10,5),    
    k VARYING CHARACTER (24),    
    l NATIONAL VARYING CHARACTER(16)，
    _id INTEGER PRIMARY KEY AUTOINCREMENT
    );

