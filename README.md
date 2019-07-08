# java-cookbook
jave cookbook, java by example, java烹饪书

## 命名规范
1. 命名使用名词
2. 驼峰命名法（Camel-Case）: 当变量名或函数名是由一个或多个单字连结在一起，而构成的唯一识别字时，首字母以小写开头，每个单词首字母大写（第一个单词除外）。如：myFirstName
3. 项目名、包名全小写。如: com.huahuayu.dao
4. 类名首字母大写。 如: StudentAnswer.java
5. 接口类：UserInterface( Dao、Service ).java   接口实现类：UserInterfaceImpl( Dao、Service ).java
6. 变量名：基本结构为typeVariableName，用3字符前缀来表示数据类型。如：定义一个整形变量：intDocCount
7. 静态变量：全部大写，多词合成的变量采用“_”来连接各单词。如：USER_LIST
8. 方法：首字母以小写开头，每个单词首字母大写（第一个单词除外）。最好是一个动词或者动词词组或者第一个单词为一个动词。如：getUserName()
9. Web层（action、controller）方法：最好是贴近web的语言，如register，login，logout
10. 服务层方法（service）：根据方法的行为命名，只描述方法的意义，而不采用方法的目的命名。比如系统的添加新用户，用户可以前台注册，也可以管理员后台添加，方法会被重用，所以最好不要用使用register，采用add会更好写。避免使用与web层相关的方法
11. 数据层方法（dao）：只能以insert（插入）,delete（删除）,update（更新）,select（查找）,count（统计）开头
12. 注释 （Javadoc）：以/**开头，而以*/结束，即 /**    */ 

## idea设置
### 插件
| 插件名                        | 功能                                             | 备注                                                               |
| ----------------------------- | ------------------------------------------------ | ------------------------------------------------------------------ |
| save actions                  | 可以定义保存代码时所做的动作                     | 安装好后不是默认开启，需自己开启                                   |
| Alibaba Java Coding Guideline | 可以检查代码是否符合阿里巴巴编码规范，并给出建议 | https://github.com/alibaba/p3c                                     |
| google-java-format            | 按google标准格式化                               | 放弃使用，因为缩进为2个空格，不习惯，国内开发规范影响大多为4个空格 |
| IdeaVim                       | vim模拟                                          |                                                                    |
| .ignore                       | ignore文件模板                                   |                                                                    |
| Relative Line Number          | 相对行号                                         |                                                                    |

### .gitignore文件  
```
# Created by .ignore support plugin (hsz.mobi)
### Java template
# Compiled class file
*.class

# Log file
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*

*.idea
*.iml
```

### module settings
1. 右键 --> Open module settings  
2. 选择jdk版本  

![](https://raw.githubusercontent.com/huahuayu/img/master/20190624220303.png)

## java语法
### helloworld
上面的例子虽然简单，但是包含了很多的知识点:
1. Java 中所有的代码都必须包含在 class 中
2. main 方法是程序的入口
3. Java 是区分大小写的，如果写成 Main，那么程序将不能运行。
4. 使用 public 修饰的 class 必须和源代码文件名相同。
``` java
public class HelloWorld{
    public static void  main(String[] args){
        System.out.println("HelloWorld!");
    }
}
```

编译源代码：打开命令行，切换到源代码目录，输入`javac HelloWorld.java`，如果程序没有任何提示，并且在同级目录下生成了一个.class 扩展名的文件，那么说明编译成功，反之编译失败。

运行程序：输入`java HelloWorld`，这个时候不需要再添加扩展名了。

```
$ javac HelloWorld.java                      
$ java HelloWorld                            
HelloWorld!
```

``` bash
$ javac HelloWorld.java                      
$ java HelloWorld                            
HelloWorld!
```

### 变量
在 Java 中，变量需要先声明(declare)才能使用。在声明中，说明变量的类型，赋予变量以特别名字，以便在后面的程序中调用它。

变量声明语法：  
``` java
int a = 1;
```

### 常量
常量代表程序运行过程中不能改变的值。我们也可以把它们理解为特殊的变量，只是它们在程序的运行过程中是不允许改变的。常量的值是不能被修改的。

Java 中的final关键字可以用于声明属性（常量），方法和类。当final修饰属性时，代表该属性一旦被分配内存空间就必须初始化, 它的含义是“这是无法改变的”或者“终态的”。在变量前面添加关键字final即可声明一个常量。在 Java 编码规范中，要求常量名必须大写。

``` java
final double PI = 3.14;
```

常量也可以先声明，再进行赋值，但只能赋值一次，比如： ​

``` java
​ final int FINAL_VARIABLE; ​ FINAL_VARIABLE = 100;
```

### 基本数据类型
Java 中一共八种基本数据类型，下表列出了基本数据类型的数据范围、存储格式、默认值、包装类型等。  

| 数据类型 | 默认值         | 存储格式 | 数据范围                                                        | 包装类型  |
| -------- | -------------- | -------- | --------------------------------------------------------------- | --------- |
| short    | 0              | 2 个字节 | -32,768 到 32767                                                | Short     |
| int      | 0              | 4 个字节 | -2,147,483,648 到 2,147,483,647                                 | Integer   |
| byte     | 0              | 1 个字节 | -128 到 127                                                     | Byte      |
| char     | 空             | 2 个字节 | Unicode 的字符范围：’\u0000’（即为 0）到’\uffff’（即为 65,535） | Character |
| long     | 0L 或 0l       | 8 个字节 | -9,223,372,036,854,775,808 到 9,223,372,036, 854,775,807        | Long      |
| float    | 0.0F 或 0.0f   | 4 个字节 | 32 位 IEEEE-754 单精度范围                                      | Float     |
| double   | 0.0 或 0.0D(d) | 8 个字节 | 64 位 IEEE-754 双精度范围                                       | Double    |
| boolean  | false          | 1 位     | true 或 false                                                   | Boolean   |

**整数**  
byte、short、int、long 四种基本数据类型表示整数，需要注意的是 long 类型，使用 long 修饰的变量需要在数值后面加上 L 或者 l，比如long num=1L;，一般使用大写 L，为了避免小写 l 与数值 1 混淆。

**浮点数**  
float 和 double 类型表示浮点数，即可以表示小数部分。需要注意的是 float 类型的数值后面需要加上 F 或者 f，否则会被当成 double 类型处理。double 类型的数值可以加上 D 或 d，也可以不加。

**char 类型**  
char 类型用于表示单个字符。需要将字符用单引号括起来char a='a'，char 可以和整数互相转换，如果字符a也可以写成char a=97。也可以用十六进制表示char a = '\u0061'。

**boolean 类型**  
boolean 类型（布尔类型）用于表示真值true或者假值false，Java 中布尔值不能和整数类型或者其它类型互相转换。

### String类型
Java 中使用 String 类来定义一个字符串，字符串是`常量`，它们的值在创建之后不能更改。字符串缓冲区支持可变的字符串。

String 对象的初始化格式有如下两种：
``` java
String s0 = "abc";

String s1 = new String("abd");
```
String 类具有丰富的方法，比如计算字符串的长度、连接字符串、比较字符串、提取字符串等等。  

#### 计算字符串长度
length()方法  
``` java
String s1 = "abc";
String s2 = "Java语言";  // 中文字符也是一个字符
int len1 = s1.length();  // 3
int len2 = s2.length(); // 6
```

#### 字符串比较
equals() 方法,该方法的作用是判断两个字符串对象的内容是否相同。如果相同则返回 true，否则返回 false。

equals() 方法比较是从第一字符开始，一个字符一个字符依次比较。

如果想忽略掉大小写关系，可以调用equalsIgnoreCase()方法，其用法与 equals 一致，不过它会忽视大小写。

``` java
public class StringTest {
    public static void main(String[] args){
        String s = new String("Java");
        String m = "java";
        System.out.println("用equals()比较，java和Java结果为"+s.equals(m));
        System.out.println("用equalsIgnoreCase()比较，java和Java结果为"+s.equalsIgnoreCase(m));
    }
}
```

编译运行  
``` bash
$ javac StringTest.java
$ java StringTest
用equals()比较，java和Java结果为false
用equalsIgnoreCase()比较，java和Java结果为true
```

而使用"=="比较的是两个对象在内存中存储的地址是否一样。例如:  

``` java
String s1 = "abc";
String s2 = new String("abc");
boolean b = (s1 == s2);
```

则变量 b 的值是 false，因为 s1 对象对应的地址是"abc"的地址，而 s2 使用 new 关键字申请新的内存，所以内存地址和 s1 的"abc"的地址不一样，所以获得的值是 false。

#### 字符串连接
字符串连接有两种方法：
1. 使用`+`，比如`String s = "Hello " + "World!"`
2. 使用 String 类的 concat() 方法
代码示例：
``` java
String s0 = new String("Hello ");
String s1 = "World" + "!";   //+号连接
String s2 = s0.concat(s1); //concat()方法连接
System.out.println(s2);
```

而且使用`+`进行连接，不仅可以连接字符串，也可以连接其他类型。但是要求进行连接时至少有一个参与连接的内容是字符串类型。

#### charAt()方法
charAt()方法的作用是按照索引值(规定字符串中第一个字符的索引值是 0，第二个字符的索引值是 1，依次类推)，获得字符串中的指定字符。例如：

``` java
String s = "abc";
char c = s.charAt(1);
```
则变量 c 的值是'b'。

#### 字符串常用提取方法
| 方法                                    | 返回值 | 功能描述                                   |
| --------------------------------------- | ------ | ------------------------------------------ |
| indexOf(int ch)                         | int    | 搜索字符 ch 第一次出现的索引               |
| indexOf(String value)                   | int    | 搜索字符串 value 第一次出现的索引          |
| lastIndexOf(int ch)                     | int    | 搜索字符 ch 最后一次出现的索引             |
| lastIndexOf(String value)               | int    | 搜索字符串 value 最后一次出现的索引        |
| substring(int index)                    | String | 提取从位置索引开始到结束的字符串           |
| substring(int beginindex, int endindex) | String | 提取[beginindex,endindex)的字符            |
| trim()                                  | String | 返回一个前后不含任何空格的调用字符串的副本 |

### 算术运算符
| 算术运算符 | 名称 | 描述                     | 类型       | 举例                 |
| ---------- | ---- | ------------------------ | ---------- | -------------------- |
| +          | 加法 | 相加运算符两侧的值       | 双目运算符 | a + b 等于 8         |
| -          | 减法 | 左操作数减去右操作数     | 双目运算符 | a - b 等于 2         |
| *          | 乘法 | 相乘操作符两侧的值       | 双目运算符 | a * b 等于 15        |
| /          | 除法 | 左操作数除以右操作数     | 双目运算符 | a / b 等于 1         |
| %          | 取余 | 左操作数除右操作数的余数 | 双目运算符 | a % b 等于 2         |
| ++         | 自增 | 操作数的值增加 1         | 单目运算符 | ++i（或 i++） 等于 2 |
| --         | 自减 | 操作数的值减少 1         | 单目运算符 | --i（或 i--） 等于 0 |

### 位运算符
| 位运算符 | 名称         | 描述                                                         | 举例                              |
| -------- | ------------ | ------------------------------------------------------------ | --------------------------------- |
| &        | 按位与       | 如果相对应位都是 1，则结果为 1，否则为 0                     | （a＆b），得到 12，即 0000 1100   |
| 丨       | 按位或       | 如果相对应位都是 0，则结果为 0，否则为 1                     | （ a 丨 b ）得到 61，即 0011 1101 |
| ^        | 按位异或     | 如果相对应位值相同，则结果为 0，否则为 1                     | （a^b）得到 49，即 0011 0001      |
| ~        | 按位补       | 翻转操作数的每一位，即 0 变成 1，1 变成 0                    | （〜a）得到-61，即 1100 0011      |
| <<       | 按位左移     | 左操作数按位左移右操作数指定的位数                           | a<<2 得到 240，即 1111 0000       |
| >>       | 按位右移     | 左操作数按位右移右操作数指定的位数                           | a>>2 得到 15 即 1111              |
| >>>      | 按位右移补零 | 左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充 | a>>>2 得到 15 即 0000 1111        |

### 逻辑运算符
| 逻辑运算符 | 名称 | 描述                                                           | 类型       | 举例             |
| ---------- | ---- | -------------------------------------------------------------- | ---------- | ---------------- |
| &&         | 与   | 当且仅当两个操作数都为真，条件才为真                           | 双目运算符 | （a && b）为假   |
| ｜｜       | 或   | 两个操作数任何一个为真，条件为真                               | 双目运算符 | （a ｜｜ b）为真 |
| ！         | 非   | 用来反转操作数的逻辑状态。如果条件为真，则逻辑非运算符将得到假 | 单目运算符 | （!a）为假       |
| ^          | 异或 | 如果两个操作数逻辑相同，则结果为假，否则为真                   | 双目运算符 | （a ^ b）为真    |

### 关系运算符
| 比较运算符 | 名称     | 描述                                                           | 举例               |
| ---------- | -------- | -------------------------------------------------------------- | ------------------ |
| ==         | 等于     | 判断两个操作数的值是否相等，如果相等则条件为真                 | （a == b）为 false |
| ！=        | 不等于   | 判断两个操作数的值是否相等，如果值不相等则条件为真             | (a != b) 为 true   |
| >          | 大于     | 判断左操作数的值是否大于右操作数的值，如果是那么条件为真       | （a > b）为 false  |
| <          | 小于     | 判断左操作数的值是否小于右操作数的值，如果是那么条件为真       | （a < b）为 true   |
| >=         | 大于等于 | 判断左操作数的值是否大于或等于右操作数的值，如果是那么条件为真 | （a >= b）为 false |
| <=         | 小于等于 | 判断左操作数的值是否小于或等于右操作数的值，如果是那么条件为真 | （a <= b）为 true  |

除了上表列出的二元运算符，Java 还有唯一的一个三目运算符 ?:  

语法格式： `布尔表达式？表达式 1 : 表达式 2`

``` java
System.out.println("a > b ? a : b = " + (a > b ? a : b));  // a>b为true，表达式的值为a，反之为b

```

**强调**:

`==`和`!=`适用于所有的基本数据类型，其他关系运算符不适用于`boolean`，因为 `boolean` 值只有`true`和`false`，比较没有任何意义。

`==`和`!=`也适用于所有对象，可以比较对象的引用是否相同。

**引用**: Java 中一切都是对象，但操作的标识符实际是对象的一个引用。

### java关键字
|           |          |            |            |              |
| --------- | -------- | ---------- | ---------- | ------------ |
| abstract  | continue | for        | new        | synchronized |
| assert*** | default  | goto*      | package    | synchronized |
| boolean   | do       | if         | private    | this         |
| break     | double   | implements | protected  | throw        |
| byte      | else     | import     | public     | throws       |
| case      | enum**** | instanceof | return     | transient    |
| catch     | extends  | int        | short      | try          |
| char      | final    | interface  | static     | void         |
| class     | finally  | long       | strictfp** | volatile     |
| const*    | float    | native     | super      | while        |

```
* not used
** added in 1.2
*** added in 1.4
**** added in 5.0
```

### 方法
Java 中的方法，可以将其看成一个功能的集合，它们是为了解决特定问题的代码组合。

方法的定义语法：

```
访问修饰符 返回值类型 方法名(参数列表){
    方法体
}
```

如：

``` java
public void functionName(Object arg){

}
```

在上面的语法说明中：

1.访问修饰符：代表方法允许被访问的权限范围， 可以是 public、protected、private 或者省略（default） ，其中 public 表示该方法可以被其他任何代码调用。

2.返回值类型：方法返回值的类型，如果方法不返回任何值，则返回值类型指定为 void (代表无类型)；如果方法具有返回值，则需要指定返回值的类型，并且在方法体中使用 return 语句返回值。

3.方法名：是方法的名字，必须使用合法的标识符。

4.参数列表：是传递给方法的参数列表，参数可以有多个，多个参数间以逗号隔开，每个参数由参数类型和参数名组成，以空格隔开。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。

5.方法体：方法体包含具体的语句，定义该方法的功能。

根据方法是否带参、是否带返回值，可将方法分为四类：

- 无参无返回值方法
- 无参带返回值方法
- 带参无返回值方法
- 带参带返回值方法

当方法定义好之后，需要调用才可以生效，我们可以通过 main 方法（mian 方法是 Java 程序的入口，所以需要用它来调用）来调用它，比如：
``` java
public class MethodDemo{
    public static void main(String[] args){
        method();
    }
    //这里要加上static关键字 应为静态方法只能调用静态方法
    public static void method(){
        System.out.println("方法被调用");
    }
}
```

### 流程控制
#### if
#### switch
#### while/do-while
#### for
#### break
#### continue

### 数组
数组，是有序的元素序列。使用数组前要先声明。

语法：

```
数据类型[ ] 数组名;   //或者: 数据类型 数组名[ ];
```

数组名为任意合法的变量名，如：

``` java
int ages[];      //存放年龄的数组，类型为整型
char symbol[];   //存放符号的数组，类型为字符型
String [] name;  //存放名称的数组，类型为字符串型
```

声明数组后，需要为数组分配空间，也就是定义多大的数组。

语法：

```
数组名 = new  数据类型 [ 数组长度 ];
```

数组长度就是数组最多可存放元素的个数。可以在数组声明的时候初始化数组，或者在声明时就为它分配好空间，这样就不用再为数组分配空间。

语法：

``` java
int [] ages = {12,18,9,33,45,60}; //声明并初始化了一个整型数组，它有6个元素
char [] symbol = new char[10] //声明并分配了一个长度为10的char型数组
```

分配空间后就可以向数组中放数据了，数组中元素都是通过下标来访问的。 如：

``` java
ages[0]=12;
```
Java 中可以将一个数组赋值给另一个数组，如：

``` java
int [] a1 = {1,2,3};
int [] a2;
a2 = a1;
```

这里只是复制了一个引用，即 a2 和 a1 是相同数组的不同名称。

**注意：**

1. 数组下标从 0 开始。所以数组的下标范围是 0 至 数组长度 -1。

2. 数组不能越界访问，否则会报错。

``` java
public class Test {
    public static void main(String[] args) {
        int [] a1 = {1,2,3};
        int [] a2;
        a2 = a1;
        for(int i = 0; i < a2.length; i++){
            a2[i]++;
        }
        for(int i = 0; i < a1.length; i++){
            System.out.println(a1[i]);
        }
    }
}
```

数组遍历的简化写法  
``` java
public class JudgePrime {
    public static void main(String[] args){
        int [] ages = {12, 18, 9, 33, 45, 60};
        int i = 1;
        for(int age:ages){
            System.out.println("数组中第"+i+"个元素是"+age);
            i++;
        }
    }
}
```

### 二维/多维数组
二维数组的赋值和遍历：  
```
public class ArrayTest {
    public static void main(String[] args) {
        String[][] name = {{"ZhaoYi", "QianEr", "SunSan"},
                {"LiSi", "ZhouWu", "WuLiu"}};
        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < 3; j++) {
                System.out.println(name[i][j]);
            }
        }
    }
}
```

### 用户输入
Java 可以使用java.util包下的Scanner类来获取用户的输入。使用import java.util.Scanner;即可导入 Scanner，使用方法示例：

``` java
import java.util.Scanner;

public class ScannerDemo {
    public static void main(String[] args) {
        Scanner in=new Scanner(System.in);
        //获取用户输入的一行数据  返回为字符串
        String s = in.nextLine();
        System.out.println(s);
        //返回用户输入的int值
        int i = in.nextInt();
        System.out.println(i);
        //循环读取int数据，当输入exit时退出循环
        while (!in.hasNext("exit")) {
            System.out.println(in.nextInt());
        }
        //关闭输入
        in.close();
    }
}
```

### 面向对象
#### 类
1. 类是相同或相似对象的一种抽象，是对象的一个模板，它描述一类对象的行为和状态。  
2. 类是具有相同属性和方法（行为）的对象的集合。  

`属性`是对象具有的特征。每个对象的每个属性都拥有特定值。我们上面讲过对象是一个具体并且确定的事物，正是对象属性的值来区分不同的对象，比如我们可以通过一个人的外貌特征区分他。  

在计算机中我们通过方法去实现对象的`行为`，而对象的方法便是对象所具有的操作，比如人会走路、会哭泣、会学习等等都是人的行为，也就是人的方法。

类就是对象的抽象(或者模板)，对象就是类的具体（或者实例）。  

**定义一个类**，主要有三个步骤：
1. 定义类名，用于区分不同的类。如下代码中 public class 后面跟的就是类名。class是声明类的关键字，类名后面跟上大括号，大括号里面就是类的一些信息。public为权限修饰符。  
``` java
public class 类名{
//定义属性部分（成员变量）
属性1的类型 属性1;
属性2的类型 属性2;
...
//定义方法部分
方法1;
方法2;
...
}
```
2. 编写类的属性。对象有什么，需要通过属性来表示。属性的定义是写在类名后面的大括号里，在定义属性时，要明确属性的类型。在一个类当中可以写一个或多个属性。当然也可以不定义属性。

3. 编写类的方法。方法也是写在大括号里面。可以定义一个方法或多个方法，当然也可以不定义方法。  

``` java
public class People{
    double height;
    int age;
    int sex;

    void cry(){
        System.out.println("i am crying!");
    }

    void laugh(){
        System.out.println("i am laughing!");
    }

    void myInfo(){
        System.out.println("my height is"+height+"cm");
        System.out.println("my age is"+age);
        if(this.sex==0)
            System.out.println("i am male");
        else
            System.out.println("i am female");
    }
}
```

没有main函数的方法类编译后是不能执行的，只能被其他类的对象调用  
``` bash
$ javac People.java                                                                      
$ java People                                                                           
Error: Main method not found in class People, please define the main method as:
   public static void main(String[] args)
or a JavaFX application class must extend javafx.application.Application
```


一个类可以包含以下类型变量：  
1. 成员变量：成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。
``` java
public class People {
	//以下都是成员变量  
	private String name;
	public int age;
	protected int weight;
	//实例方法
	public String getName(){
		return this.name;
	}
```
2. 局部变量：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。
``` java
public class Calculator {
	public int input;
	public String addOne(){
        int i = 1;  // 局部变量  
		return input + i;
	}
```

3. 类变量：也叫静态变量，类变量也声明在类中，方法体之外，但必须声明为 static 类型。静态变量在内存中只有一个拷贝（节省内存），JVM只为静态分配一次内存，在加载类的过程中完成静态变量的内存分配，可用类名直接访问（方便），当然也可以通过对象来访问（但是这是不推荐的）  
``` java
public class TestClass {
    public static int i = 0;
    private static int j = 1;
}
```

#### 对象
创建对象的语法如下：  
```
类名 对象名 = new 类名();
```

定义类的时候不会为类开辟内存空间，但是一旦创建了对象，系统就会在内存中为对象开辟一块空间，用来存放对象的属性值和方法。

类定义：  
``` java
public class People{
    double height;
    int age;
    int sex;

    void cry(){
        System.out.println("i am crying!");
    }

    void laugh(){
        System.out.println("i am laughing!");
    }

    void myInfo(){
        System.out.println("my height is "+height+"cm");
        System.out.println("my age is "+age);
        if(this.sex==0)
            System.out.println("i am male");
        else
            System.out.println("i am female");
    }
}
```

People类的对象定义和使用：
``` java
public class NewObject {
    public static void main(String[] args) {
        People alice = new People(); //创建一个People对象alice

        alice.height =170;
        alice.age = 20;
        alice.sex = 1;

        alice.myInfo();
    }
}
```

#### 构造方法
每个类都有构造方法，在创建该类的对象的时候他们将被调用，如果没有定义构造方法，Java 编译器会提供一个默认构造方法。 创建一个对象的时候，至少调用一个构造方法。比如在新建一个对象new Object()，括号中没有任何参数，代表调用一个无参构造方法（默认构造方法就是一个无参构造方法）。构造方法的名称必须与类名相同，一个类可以定义多个构造方法。  

构造方法的具体内容：

1. 构造方法的名称与类名相同，且没有返回值。它的语法格式如下：
``` java
//与类同名，可以指定参数，没有返回值
public 构造方法名(){
//初始化代码
}
```

构造方法举例：  
``` java
public class People {
//属性（成员变量）有什么
    double height;     //身高
    int age;           //年龄
    int sex;       //性别，0为男性，非0为女性

    public People(){  // 默认构造方法
    }

    //带参数的构造方法，初始化了所有属性
    public People(double height, int age, int sex){
        this.height = height;  // this指带本类的对象
        this.age = age;
        this.sex = sex;
    }
}
```

有了构造方法，新建对象时就可以调用构造方法进行对象的初始化：  
``` java
//创建对象，调用我们自己定义的有参构造方法
People alice = new People(168, 21, 1);
```

通过new关键字将类实例化成对象，而new后面跟的就是构造方法。于是可以知道new + 构造方法可以创建一个新的对象。

2. 如果在定义类的时候没有写构造方法，系统会默认生成一个无参构造方法，这个构造方法什么也不会做。

3. 当有指定的构造方法时，系统都不会再添加无参构造方法了。

4. 构造方法的重载：方法名相同，但参数不同的多个方法，调用时会自动根据不同的参数选择相应的方法。

#### 引用与对象实例
新建对象实例时，实际alice保存的是People对象的引用（指针）   
``` java
People alice=new People();
```

下面例子alice2=alice1，他们保存了同一个对象的引用，改变alice1的成员变量值，alice2的成员变量值也会一起被修改  
```
People alice1=new People();
People alice2=alice1;
System.out.println(alice1==alice2);  // true, 因为他们是指向同一个对象
```

#### static关键字
static意味着，该成员属性/方法归属于类，而不是某个对象所有，所以可以使用`类名.静态成员/方法`直接访问。
**静态成员**
Java 中被 `static` 修饰的成员称为静态成员或类成员。它属于整个类所有，而不是某个对象所有，即被类的所有对象所共享。静态成员可以使用类名直接访问，也可以使用对象名进行访问。  
``` java
public class StaticTest{
    public static String string="shiyanlou";
    public static void main(String[] args){
        //静态成员不需要实例化 直接就可以访问
        System.out.println(StaticTest.string);
        //如果不加static关键字 需要这样访问
        StaticTest staticTest=new StaticTest();
        System.out.println(staticTest.string);
        //如果加上static关键字，上面的两种方法都可以使用
    }
}
```

**静态方法**
被 `static` 修饰的方法是静态方法，静态方法不依赖于对象，不需要将类实例化便可以调用，由于不实例化也可以调用，所以不能有 this，也不能访问非静态成员变量和非静态方法。但是非静态成员变量和非静态方法可以访问静态方法。

#### final关键字
final意味着值不能被改变，是最终值，是常量。  
`final`关键字可以修饰类、方法、属性和变量：  
1. final 修饰类，则该类不允许被继承，为最终类
2. final 修饰方法，则该方法不允许被覆盖（重写）
3. final 修饰属性：则该类的属性不会进行隐式的初始化（类的初始化属性必须有值）或在构造方法中赋值（但只能选其一）
4. final 修饰变量，则该变量的值只能赋一次值，即常量

#### 访问修饰符
| 修饰符    | 本类 | 同包 | 子类 | 其他 |
| --------- | ---- | ---- | ---- | ---- |
| private   | √    |      |      |      |
| 默认      | √    | √    |      |      |
| protected | √    | √    | √    |      |
| public    | √    | √    | √    | √    |


#### 封装
封装，即隐藏对象的属性和实现细节，仅对外公开接口，控制在程序中属性的读和修改的访问级别。  
这样做有什么好处？
1. 只能通过规定的方法访问数据
2. 隐藏类的实例细节，方便修改和实现。

我们在开汽车的时候，只用去关注如何开车，我们并不在意车子是如何实现的，这就是封装。  

如何去实现类的封装呢？

1. 修改属性的可见性，在属性的前面添加修饰符(private)
2. 对每个值属性提供对外的公共方法访问，如创建 getter/setter（取值和赋值） 方法，用于对私有属性的访问
3. 在 getter/setter 方法里加入属性的控制语句，例如我们可以加一个判断语句，对于非法输入给予否定。

``` java
public class People {
//属性（成员变量）有什么，前面添加了访问修饰符private
//变成了私有属性，必须通过方法调用
    private double height;     //身高

//属性已经封装好了，如果用户需要调用属性
//必须用getter和setter方法进行调用
//getter和setter方法需要程序员自己定义
    public double getHeight(){    
    //getter 方法命名是get关键字加属性名（属性名首字母大写）
    //getter 方法一般是为了得到属性值
        return height;
    }

//同理设置我们的setter方法
//setter 方法命名是set关键字加属性名（首字母大写）
//setter 方法一般是给属性值赋值，所以有一个参数
    public void setHeight(double newHeight){
        height = newHeight;
    }
}
```

现在 main 函数里的对象，不能再直接调用属性了，只能通过getter和setter方法进行调用。  
``` java
public class NewObject {

    public static void main(String[] args) {
        People LiLei = new People();    //创建了一个People对象LiLei

        //利用setter方法为属性赋值
        LiLei.setHeight(170.0);

        //利用getter方法取属性值
        System.out.println("LiLei的身高是"+LiLei.getHeight());
    }
}
```

#### this
this关键字代表当前对象。使用this.属性操作当前对象的属性，this.方法调用当前对象的方法。

用private修饰的属性，必须定义 getter 和 setter 方法才可以访问到(Eclipse IDEA 等 IDE 都有自动生成 getter 和 setter 方法的功能)。

``` java
    public void setAge(int age) {
        this.age = age;
    }
    public int getAge() {
        return age;
    }
```

创建好了 getter 和 setter 方法后，我们发现方法中参数名和属性名一样。

当成员变量和局部变量之间发生冲突时，在属性名前面添加了this关键字。 此时就代表将一个参数的值赋给当前对象的属性。同理this关键字可以调用当前对象的方法.

#### 继承
继承可以看成是类与类之间的衍生关系。比如狗类是动物类，牧羊犬类又是狗类。于是我们可以说狗类继承了动物类，而牧羊犬类就继承了狗类。于是狗类就是动物类的子类（或派生类），动物类就是狗类的父类（或基类）。

所以继承需要符合的关系是：is-a，父类更通用，子类更具体。

语法：
``` java
class 子类 extends 父类
```

动物类：   
``` java
public class Animal {
    public int legNum;     //动物四肢的数量

    //类方法
    public void bark() {
        System.out.println("动物叫！");
    }
}
```

子类Dog继承动物类：  
```
public class Dog extends Animal {
}
```

Dog 类继承了父类 Animal，我们 Dog 类里什么都没有写，其实它继承了父类 Animal，所以 Dog 类拥有 Animal 类的全部方法和属性。测试一下：  
``` java
public class Test{
    public static void main(String[] args) {
        Dog a = new Dog();
        a.legNum = 4;
        a.bark();
    }
}
```
**为什么需要继承？**

如果有两个类相似，那么它们会有许多重复的代码，导致后果就是代码量大且臃肿，后期的维护性不高。通过继承就可以解决这个问题，将两段代码中相同的部分提取出来组成一个父类，实现代码的复用。

**继承的特点：**

1. 子类拥有父类除 private 以外的所有属性和方法
2. 子类可以拥有自己的属性和方法
3. 子类可以重写实现父类的方法
4. Java 中的继承是单继承，一个类只有一个父类

Java **不支持多继承**，但支持多重继承（组合）。
![](https://raw.githubusercontent.com/huahuayu/img/master/20190628133057.png)

Java **实现多继承的一个办法**是 implements（实现）接口

#### super关键字
super关键字来实现对父类成员的访问，用来引用当前对象的父类。
``` java
class Animal {
  void eat() {
    System.out.println("animal : eat");
  }
}
 
class Dog extends Animal {
  void eat() {
    System.out.println("dog : eat");
  }
  void eatTest() {
    this.eat();   // this 调用自己的方法
    super.eat();  // super 调用父类方法
  }
}
 
public class Test {
  public static void main(String[] args) {
    Animal a = new Animal();
    a.eat();
    Dog d = new Dog();
    d.eatTest();
  }
}

/*
output:
animal : eat
dog : eat
animal : eat
*/
```

#### 构造方法与继承
子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 super 关键字调用父类的构造器并配以适当的参数列表。  

如果父类构造器没有参数，则在子类的构造器中不需要使用 super 关键字调用父类构造器，系统会自动调用父类的无参构造器。  
``` java
class SuperClass {
  private int n;
  SuperClass(){
    System.out.println("SuperClass()");
  }
  SuperClass(int n) {
    System.out.println("SuperClass(int n)");
    this.n = n;
  }
}
// SubClass 类继承
class SubClass extends SuperClass{
  private int n;
  
  SubClass(){ // 自动调用父类的无参数构造器
    System.out.println("SubClass");
  }  
  
  public SubClass(int n){ 
    super(300);  // 调用父类中带有参数的构造器
    System.out.println("SubClass(int n):"+n);
    this.n = n;
  }
}
// SubClas2 类继承
class SubClass2 extends SuperClass{
  private int n;
  
  SubClass2(){
    super(300);  // 调用父类中带有参数的构造器
    System.out.println("SubClass2");
  }  
  
  public SubClass2(int n){ // 自动调用父类的无参数构造器
    System.out.println("SubClass2(int n):"+n);
    this.n = n;
  }
}
public class TestSuperSub{
  public static void main (String args[]){
    System.out.println("------SubClass 类继承------");
    SubClass sc1 = new SubClass();
    SubClass sc2 = new SubClass(100); 
    System.out.println("------SubClass2 类继承------");
    SubClass2 sc3 = new SubClass2();
    SubClass2 sc4 = new SubClass2(200); 
  }
}

/*
输出的结果为：
------SubClass 类继承------
SuperClass()
SubClass
SuperClass(int n)
SubClass(int n):100
------SubClass2 类继承------
SuperClass(int n)
SubClass2
SuperClass()
SubClass2(int n):200
*/
```

#### 方法重载
方法重载是指在一个类中定义多个同名的方法，但要求每个方法具有不同的参数的类型或参数的个数。方法重载一般用于创建一组任务相似但是参数不同的方法。  
``` java
public class Test {
    void f(int i) {
        System.out.println("i=" + i);
    }

    void f(float f) {
        System.out.println("f=" + f);
    }

    void f(String s) {
        System.out.println("s=" + s);
    }

    void f(String s1, String s2){
        System.out.println("s1+s2="+(s1+s2));
    }

    void f(String s, int i){
        System.out.println("s="+s+",i="+i);
    }

    public static void main(String[] args) {
        Test test = new Test();
        test.f(3456);
        test.f(34.56f);
        test.f("abc");
        test.f("abc","def");
        test.f("abc",3456);
    }
}

/*
result:
i=3456
f=34.56
s=abc
s1+s2=abcdef
s=abc,i=3456
*/
```

方法重载有以下几种规则：

1. 方法中的参数列表必须不同。比如：参数个数不同或者参数类型不同。
2. 重载的方法中允许抛出不同的异常
3. 可以有不同的返回值类型，但是参数列表必须不同
4. 可以有不同的访问修饰符

#### 方法重写
子类可以继承父类的方法，但如果子类对父类的方法不满意，想在里面加入适合自己的一些操作时，就需要将方法进行重写。并且子类在调用方法中，优先调用子类的方法。

比如 Animal 类中有bark()这个方法代表了动物叫，但是不同的动物有不同的叫法，比如狗是汪汪汪，猫是喵喵喵。

当然在方法重写时要注意，重写的方法一定要与原父类的方法语法保持一致，比如返回值类型，参数类型及个数，和方法名都必须一致。

例如：
``` java
public class Animal {
    //类方法
    public void bark() {
        System.out.println("动物叫！");
    }
}

public class Dog extends Animal {
       //重写父类的bark方法
        public void bark() {
        System.out.println("汪！汪！汪！");
    }
}

public class Test{
    public static void main(String args[]){
           Animal a = new Animal(); // Animal 对象
        Dog d = new Dog();   // Dog 对象

          Animal b = new Dog(); // Dog 对象,向上转型为Animal类型，具体会在后面的内容进行详解

          a.bark();// 执行 Animal 类的方法
         d.bark();//执行 Dog 类的方法
          b.bark();//执行 Dog 类的方法
       }
}

/*
动物叫！
汪！汪！汪！
汪！汪！汪！
*/
```

#### 多态
多态是指允许不同类的对象对同一消息做出响应。即同一消息可以根据发送对象的不同而采用多种不同的行为方式。多态也称作动态绑定（dynamic binding），是指在执行期间判断所引用对象的实际类型，根据其实际的类型调用其相应的方法。

通俗地讲，只通过父类就能够引用不同的子类，这就是多态，我们只有在运行的时候才会知道引用变量所指向的具体实例对象。

#### 向上转型

``` java
class Animal {
    //父类方法
    public void bark() {
        System.out.println("动物叫！");
    }
}

class Dog extends Animal {

    //子类重写父类的bark方法
    public void bark() {
        System.out.println("汪、汪、汪！");
    }
    //子类自己的方法
    public void dogType() {
        System.out.println("这是什么品种的狗？");
    }
}


public class Test {

    public static void main(String[] args) {
        Animal a = new Animal();
        Animal b = new Dog();
        Dog d = new Dog(); 

        a.bark();
        b.bark();
        //b.dogType(); 编译不通过
        d.bark();
        d.dogType();
    }

}

/*
动物叫！
汪、汪、汪！
汪、汪、汪！
这是什么品种的狗？
*/
```

在这里，由于 b 是父类的引用，指向子类的对象，因此不能获取子类的方法（dogType()方法）,同时当调用 bark()方法时，由于子类重写了父类的 bark()方法,所以调用子类中的 bark()方法。

向上转型，在运行时，会遗忘子类对象中与父类对象中不同的方法，也会覆盖与父类中相同的方法——重写。

**多态存在的三个必要条件:**  
1. 继承
2. 重写
3. 父类引用指向子类对象

**多态的实现方式:**
1. 继承父类进行方法重写  
2. 抽象类和抽象方法  
3. 接口实现  


#### 抽象类
在定义类时，前面加上abstract关键字修饰的类叫抽象类。 抽象类中有抽象方法，这种方法是不完整的，仅有声明而没有方法体。抽象方法声明语法如下：

``` java
abstract void f();  //f()方法时抽象方法
```

那我们什么时候会用到抽象类呢？

1. 在某些情况下，某个父类只是知道其子类应该包含怎样的方法，但无法准确知道这些子类如何实现这些方法。也就是说抽象类是约束子类必须要实现哪些方法，而并不关注方法如何去实现。
2. 从多个具有相同特征的类中抽象出一个抽象类，以这个抽象类作为子类的模板，从而避免了子类设计的随意性。

所以由上可知，抽象类是限制规定子类必须实现某些方法，但不关注实现细节。

``` java
//抽象方法
public abstract class TelePhone {
    public abstract void call();  //抽象方法,打电话
    public abstract void message(); //抽象方法，发短信
}

public class CellPhone extends TelePhone {

    @Override
    public void call() {
        System.out.println("我可以打电话！");
    }

    @Override
    public void message() {
        System.out.println("我可以发短信！");
    }

    public static void main(String[] args) {
        CellPhone cp = new CellPhone();
        cp.call();
        cp.message();
    }

}
```

#### 接口
接口用于描述类所具有的功能，而不提供功能的实现，功能的实现需要写在实现接口的类中，并且该类必须实现接口中所有的未实现方法。

接口的声明语法格式如下：
``` java
修饰符 interface 接口名称 [extends 其他的接口名] {
        // 声明变量
        // 抽象方法
}
```

声明一个Animal接口：  
``` java
// Animal.java
interface Animal {
        //int x;
        //编译错误,x需要初始化，因为是 static final 类型
        int y = 5;
        public void eat();
        public void travel();
}
```
**注意点**：在`Java8`中

1. 接口不能用于实例化对象
2. 接口中方法只能是抽象方法、default 方法、静态方法
3. 接口成员是 static final 类型
4. 接口支持多继承

在`Java9`中，接口可以拥有私有方法和私有静态方法，但是只能被该接口中的 default 方法和静态方法使用。

**多继承的实现方式**
``` java
修饰符 interface A extends 接口1，接口2{

}

修饰符 class A implements 接口1，接口2{

} 
```

#### 接口与抽象类的区别
抽象类和接口的区别
1. 抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
2. 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 public static final 类型的。
3. 接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
4. 一个类只能继承一个抽象类，而一个类却可以实现多个接口。

#### 内部类
将一个类的定义放在另一个类的定义内部，这就是内部类。而包含内部类的类被称为外部类。  

内部类的主要作用如下：
1. 内部类提供了更好的封装，可以把内部类隐藏在外部类之内，不允许同一个包中的其他类访问该类
2. 内部类的方法可以直接访问外部类的所有数据，包括私有的数据
3. 内部类所实现的功能使用外部类同样可以实现，只是有时使用内部类更方便
4. 内部类允许继承多个非接口类型

>注：内部类是一个编译时的概念，一旦编译成功，就会成为完全不同的两类。对于一个名为 outer 的外部类和其内部定义的名为 inner 的内部类。编译完成后出现 outer.class 和 outer$inner.class 两类。所以内部类的成员变量/方法名可以和外部类的相同。

``` java
// People.java
//外部类People
public class People {
    private String name = "LiLei";         //外部类的私有属性
    //内部类Student
    public class Student {
        String ID = "20151234";               //内部类的成员属性
        //内部类的方法
        public void stuInfo(){
            System.out.println("访问外部类中的name：" + name);
            System.out.println("访问内部类中的ID：" + ID);
        }
    }

    //测试成员内部类
    public static void main(String[] args) {
        People a = new People();     //创建外部类对象，对象名为a
        Student b = a.new Student(); //使用外部类对象创建内部类对象，对象名为b
        // 或者为 People.Student b = a.new Student();
        b.stuInfo();   //调用内部对象的suInfo方法
    }
}
```

成员内部类的使用方法：

1. Student 类相当于 People 类的一个成员变量，所以 Student 类可以使用任意访问修饰符
2. Student 类在 People 类里，所以访问范围在类里的所有方法均可以访问 People 的属性（即内部类里可以直接访问外部类的方法和属性，反之不行）
3. 定义成员内部类后，必须使用外部类对象来创建内部类对象，即 内部类 对象名 = 外部类对象.new 内部类();
4. 如果外部类和内部类具有相同的成员变量或方法，内部类默认访问自己的成员变量或方法，如果要访问外部类的成员变量，可以使用 this 关键字 如上述代码中：a.this

#### 静态内部类
``` java
// People.java
//外部类People
public class People {
    private String name = "LiLei";         //外部类的私有属性

/*外部类的静态变量。
Java 中被 static 修饰的成员称为静态成员或类成员。它属于整个类所有，而不是某个对象所有，即被类的所有对象所共享。静态成员可以使用类名直接访问，也可以使用对象名进行访问。
*/
    static String ID = "510xxx199X0724XXXX"; 

    //静态内部类Student
    public static class Student {
        String ID = "20151234";               //内部类的成员属性
        //内部类的方法
        public void stuInfo(){
            System.out.println("访问外部类中的name：" + (new People().name));
            System.out.println("访问外部类中的ID：" + People.ID);
            System.out.println("访问内部类中的ID：" + ID);
        }
    }

    //测试成员内部类
    public static void main(String[] args) {
        Student b = new Student();   //直接创建内部类对象，对象名为b
        b.stuInfo();                 //调用内部对象的suInfo方法
    }
}
```

静态内部类是 static 修饰的内部类，这种内部类的特点是：

1. 静态内部类不能直接访问外部类的非静态成员，但可以通过 new 外部类().成员 的方式访问
2. 如果外部类的静态成员与内部类的成员名称相同，可通过类名.静态成员访问外部类的静态成员；如果外部类的静态成员与内部类的成员名称不相同，则可通过成员名直接调用外部类的静态成员
3. 创建静态内部类的对象时，不需要外部类的对象，可以直接创建 内部类 对象名= new 内部类();

#### 局部内部类
局部内部类，是指内部类定义在方法和作用域内。
``` java
// People.java
//外部类People
public class People {    
    //定义在外部类中的方法内：
    public void peopleInfo() {
        final String sex = "man";  //外部类方法中的常量
        class Student {
            String ID = "20151234"; //内部类中的常量
            public void print() {
                System.out.println("访问外部类的方法中的常量sex：" + sex);
                System.out.println("访问内部类中的变量ID:" + ID);
            }
        }
        Student a = new Student();  //创建方法内部类的对象
        a.print();//调用内部类的方法
    }
    //定义在外部类中的作用域内
    public void peopleInfo2(boolean b) {
        if(b){
            final String sex = "man";  //外部类方法中的常量
            class Student {
                String ID = "20151234"; //内部类中的常量
                public void print() {
                    System.out.println("访问外部类的方法中的常量sex：" + sex);
                    System.out.println("访问内部类中的变量ID:" + ID);
                }
            }
            Student a = new Student();  //创建方法内部类的对象
            a.print();//调用内部类的方法
        }
    }
    //测试方法内部类
    public static void main(String[] args) {
        People b = new People(); //创建外部类的对象
        System.out.println("定义在方法内：===========");
        b.peopleInfo();  //调用外部类的方法
        System.out.println("定义在作用域内：===========");
        b.peopleInfo2(true);
    }
}
```

局部内部类也像别的类一样进行编译，但只是作用域不同而已，只在该方法或条件的作用域内才能使用，退出这些作用域后无法引用的。

#### 匿名内部类
匿名内部类，顾名思义，就是没有名字的内部类。正因为没有名字，所以匿名内部类只能使用一次，它通常用来简化代码编写。但使用匿名内部类还有个前提条件：必须继承一个父类或实现一个接口。  

``` java
// Outer.java
public class Outer { 

    public Inner getInner(final String name, String city) { 
        return new Inner() { 
            private String nameStr = name; 
            public String getName() { 
                return nameStr; 
            } 
        };
    } 

    public static void main(String[] args) { 
        Outer outer = new Outer(); 
        Inner inner = outer.getInner("Inner", "NewYork"); 
        System.out.println(inner.getName()); 
    } 
} 
interface Inner { 
    String getName(); 
}

// 运行结果：Inner
```

匿名内部类是不能加访问修饰符的。要注意的是，new 匿名类，这个类是要先定义的,如果不先定义，编译时会报错该类找不到。

同时，在上面的例子中，当所在的方法的形参需要在内部类里面使用时，该形参必须为final。这里可以看到形参 name 已经定义为 final 了，而形参 city 没有被使用则不用定义为 final。

然而，因为匿名内部类没名字，是用默认的构造函数的，无参数的，如果需要该类有带参数的构造函数，示例如下：

``` java
   public Inner getInner(final String name, String city) { 
        return new Inner(name, city) { 
            private String nameStr = name; 

            public String getName() { 
                return nameStr; 
            } 
        }; 
    } 
```

注意这里的形参 city，由于它没有被匿名内部类直接使用，而是被抽象类 Inner 的构造函数所使用，所以不必定义为 final。

#### 包
为了更好地组织类，Java 提供了包机制，用于区别类名的命名空间。

**包的作用**

1. 把功能相似或相关的类或接口组织在同一个包中，方便类的查找和使用。
2. 包采用了树形目录的存储方式。同一个包中的类名字是不同的，不同的包中的类的名字是可以相同的，当同时调用两个不同包中相同类名的类时，应该加上包名加以区别。
3. 包也限定了访问权限，拥有包访问权限的类才能访问某个包中的类。

定义包的语法：  
``` java
package 包名
//注意：必须放在源程序的第一行，包名可用"."号隔开
```

接口
``` java
/* File name : Animal.java */
package animals;

interface Animal {
   public void eat();
   public void travel();
}
```

实现类

``` java
package animals;
/* File name : MammalInt.java */

public class MammalInt implements Animal {

   public void eat() {
      System.out.println("Mammal eats");
   }

   public void travel() {
      System.out.println("Mammal travels");
   } 

   public int noOfLegs() {
      return 0;
   }

   public static void main(String args[]) {
      MammalInt m = new MammalInt();
      m.eat();
      m.travel();
   }
} 
```

用以下语句编译程序会在当前目录新建文件夹`Animals`，然后生成`Animal.class`和`MammalInt.class`文件。  
``` bash
$ javac -d . Animal.java 
$ javac -d . MammalInt.java
```

#### import
如果要使用别的包的类，需要使用`import`导入。
``` java
import java.util.Scanner;

class MyClass {
  public static void main(String[] args) {
    Scanner myObj = new Scanner(System.in);
    System.out.println("Enter username");

    String userName = myObj.nextLine(); 
    System.out.println("Username is: " + userName); 
  }
}
```

### 常用类
Java 类库提供了不少常用类，可以在编程中直接调用使用。以下是一些常用类：  
- Arrays
- StringBuilder
- Calendar
- Date
- Math
- System
- Random

#### Arrays
Arrays 类包含用于操作数组的各种方法（例如排序和搜索）。还包含一个静态工厂，允许将数组转为 List。

| 方法                                       | 描述               |
|------------------------------------------|------------------|
| <T> List<T> asList(T... a)               | 返回由指定数组构造的List   |
| void sort(Object[] a)                    | 对数组进行排序          |
| void fill(Object[] a, Object val)        | 为数组的所有元素都赋上相同的值  |
| boolean equals(Object[] a, Object[] a2)  | 检查两个数组是否相等       |
| int binarySearch(Object[] a, Object key) | 对排序后的数组使用二分法查找数据 |

``` java
import java.util.Arrays;
import java.util.Random;

public class ArraysDemo {
    public static void main(String[] args) {
        int[] arr = new int[10];
        //将数组元素都设为9
        Arrays.fill(arr, 9);
        System.out.println("fill:" + Arrays.toString(arr));
        Random random = new Random();
        for (int i = 0; i < arr.length; i++) {
            //使用100以内的随机数赋值数组
            arr[i] = random.nextInt(101);
        }
        //重新赋值后的数组
        System.out.println("重新赋值：" + Arrays.toString(arr));
        //将索引为5的元素设为50
        arr[5] = 50;
        //排序
        Arrays.sort(arr);
        //排序后的数组
        System.out.println("sort排序后：" + Arrays.toString(arr));
        //查找50的位置
        int i = Arrays.binarySearch(arr, 50);
        System.out.println("值为50的元素索引："+i);
        //复制一份新数组
        int[] newArr = Arrays.copyOf(arr, arr.length);
        //比较
        System.out.println("equals:"+Arrays.equals(arr, newArr));
    }
}
```

#### StringBuilder
StringBuilder 类是可变的。它是 String 的对等类，它可以增加和编写字符的可变序列，并且能够将字符插入到字符串中间或附加到字符串末尾（当然是不用创建其他对象的）

StringBuilder的构造方法：  

| 构造方法                            | 说明                                            |
|---------------------------------|-----------------------------------------------|
| StringBuilder()                 | 构造一个其中不带字符的 StringBuilder，其初始容量为 16 个字符       |
| StringBuilder(CharSequence seq) | 构造一个 StringBuilder，它包含与指定的 CharSequence 相同的字符 |
| StringBuilder(int capacity)     | 构造一个具有指定初始容量的 StringBuilder                   |
| StringBuilder(String str)       | 并将其内容初始化为指定的字符串内容                             |

StringBuilder类的常用方法：  

| 方法                                      | 返回值           | 功能描述                                                  |
|-----------------------------------------|---------------|-------------------------------------------------------|
| insert(int offsetm,Object obj)          | StringBuilder | 在 offsetm 的位置插入字符串 obj                                |
| append(Object obj)                      | StringBuilder | 在字符串末尾追加字符串 obj                                       |
| length()                                | int           | 确定 StringBuilder 对象的长度                                |
| setCharAt(int index,char ch)            | void          | 使用 ch 指定的新值设置 index 指定的位置上的字符                         |
| toString()                              | String        | 转换为字符串形式                                              |
| reverse()                               | StringBuilder | 反转字符串                                                 |
| delete(int start, int end)              | StringBuilder | 删除调用对象中从 start 位置开始直到 end 指定的索引（end-1）位置的字符序列         |
| replace(int start, int end, String str) | StringBuilder | 使用一组字符替换另一组字符。将用替换字符串从 start 指定的位置开始替换，直到 end 指定的位置结束 |

举例：  
``` java
public class StringBuilderTest {

    public static void main(String[] args){
        //定义和初始化一个StringBuilder类的字串s
        StringBuilder s = new StringBuilder("I");
        //在s后面添加字串" java"
        s.append(" java");
        //在s[1]的位置插入字串
        s.insert(1, " love");
        String t = s.toString(); //转为字符串
        System.out.println(t);
    }
}
```

#### String vs StingBuilder vs StringBuffer
String - 不可更改的  
StringBuilder - 可更改的  
StringBuffer - 可更改的且线程安全  
``` java
class Geeksforgeeks 
{ 
    // Concatenates to String 
    public static void concat1(String s1) 
    { 
        s1 = s1 + "forgeeks"; 
    } 
  
    // Concatenates to StringBuilder 
    public static void concat2(StringBuilder s2) 
    { 
        s2.append("forgeeks"); 
    } 
  
    // Concatenates to StringBuffer 
    public static void concat3(StringBuffer s3) 
    { 
        s3.append("forgeeks"); 
    } 
  
    public static void main(String[] args) 
    { 
        String s1 = "Geeks"; 
        concat1(s1);  // s1 is not changed, because String is immutable 
        System.out.println("String: " + s1); 
  
        StringBuilder s2 = new StringBuilder("Geeks"); 
        concat2(s2); // s2 is changed, because StringBuilder is mutable 
        System.out.println("StringBuilder: " + s2); 
  
        StringBuffer s3 = new StringBuffer("Geeks"); 
        concat3(s3); // s3 is changed, mutable and thread safe 
        System.out.println("StringBuffer: " + s3); 
    } 
} 

/** 
output:
String: Geeks
StringBuilder: Geeksforgeeks
StringBuffer: Geeksforgeeks
*/
```

**String to StringBuilder or StringBuffer**  

``` java
public class Test  
{ 
    public static void main(String[] args) 
    { 
        String str = "Geeks"; 
          
        // conversion from String object to StringBuffer 
        StringBuffer sbr = new StringBuffer(str); 
        sbr.reverse(); 
        System.out.println(sbr); 
          
        // conversion from String object to StringBuilder 
        StringBuilder sbl = new StringBuilder(str); 
        sbl.append("ForGeeks"); 
        System.out.println(sbl); 
    } 
} 

/**
output:
skeeG
GeeksForGeeks
*/
```

**StringBuffer and StringBuilder to String**  
``` java
public class Test  
{ 
    public static void main(String[] args) 
    { 
        StringBuffer sbr = new StringBuffer("Geeks"); 
        StringBuilder sbdr = new StringBuilder("Hello"); 
          
        // conversion from StringBuffer object to String 
        String str = sbr.toString(); 
        System.out.println("StringBuffer object to String : "); 
        System.out.println(str); 
          
        // conversion from StringBuilder object to String 
        String str1 = sbdr.toString(); 
        System.out.println("StringBuilder object to String : "); 
        System.out.println(str1); 
          
        // changing StringBuffer object sbr 
        // but String object(str) doesn't change 
        sbr.append("ForGeeks"); 
        System.out.println(sbr); 
        System.out.println(str); 
          
    } 
} 

/**
output:
StringBuffer object to String : 
Geeks
StringBuilder object to String : 
Hello
GeeksForGeeks
Geeks
*/

**StringBuffer to StringBuilder or vice-versa**
``` java
public class Test  
{ 
    public static void main(String[] args) 
    { 
        StringBuffer sbr = new StringBuffer("Geeks"); 
          
        // conversion from StringBuffer object to StringBuilder 
        String str = sbr.toString(); 
        StringBuilder sbl = new StringBuilder(str); 
          
        System.out.println(sbl); 
          
    } 
} 

/**
output:
Geeks
*/
```

#### Calendar
在早期的 JDK 版本中，Date 类附有两大功能： 　　

允许用年、月、日、时、分、秒来解释日期
允许对表示日期的字符串进行格式化和句法分析
在 JDK1.1 中提供了类 Calendar 来完成第一种功能，类 DateFormat 来完成第二项功能。DateFormat 是 java.text 包中的一个类。与 Date 类有所不同的是，DateFormat 类可以接受用各种语言和不同习惯表示的日期字符串。

但是 Calendar 类是一个抽象类，它完成 Date 类与普通日期表示法之间的转换，而我们更多的是使用 Calendar 类的子类 GregorianCalendar 类。它实现了世界上普遍使用的公历系统。当然我们也可以继承 Calendar 类，然后自己定义实现日历方法。

GregorianCalendar 类的构造函数：

| 构造方法                                            | 说明                                               |
|-------------------------------------------------|--------------------------------------------------|
| GregorianCalendar()                             | 创建的对象中的相关值被设置成指定时区，缺省地点的当前时间，即程序运行时所处的时区、地点的当前时间 |
| GregorianCalendar(TimeZone zone)                | 创建的对象中的相关值被设置成指定时区 zone，缺省地点的当前时间                |
| GregorianCalendar(Locale aLocale)               | 创建的对象中的相关值被设置成缺省时区，指定地点 aLocale 的当前时间            |
| GregorianCalendar(TimeZone zone,Locale aLocale) | year - 创建的对象中的相关值被设置成指定时区，指定地点的当前时间              |


TimeZone 是 java.util 包中的一个类，其中封装了有关时区的信息。每一个时区对应一组 ID。类 TimeZone 提供了一些方法完成时区与对应 ID 两者之间的转换。

例如：
``` java
//太平洋时区的 ID 为 PST
TimeZone tz0 = TimeZone.getTimeZone("PST")
//getDefault()可以获取主机所处时区的对象
TimeZone tz1 = TimeZone.getDefault()
```

Locale 只是一种机制，它用来标识一个特定的地理、政治或文化区域获取一个 Locale 对象的构造方法：

``` java
//调用Locale类的构造方法
Locale l0 = new Locale(String language)
Locale l1 = new Locale(String language, String country)
Locale l2 = new Locale(String languge, String country, String variant)

//调用Locale类中定义的常量
Locale  l1 = Locale.CHINA
```

Calendar编程示例：  
``` java
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

public class CalendarDemo {
    public static void main(String[] args) {
        System.out.println("完整显示日期时间：");
        // 字符串转换日期格式
        DateFormat fdate = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String str = fdate.format(new Date());
        System.out.println(str);

        // 创建 Calendar 对象
        Calendar calendar = Calendar.getInstance();
        // 初始化 Calendar 对象，但并不必要，除非需要重置时间
        calendar.setTime(new Date());

        // 显示年份
        System.out.println("年： " + calendar.get(Calendar.YEAR));

        // 显示月份 (从0开始, 实际显示要加一)
        System.out.println("月： " + calendar.get(Calendar.MONTH));


        // 当前分钟数
        System.out.println("分钟： " + calendar.get(Calendar.MINUTE));

        // 今年的第 N 天
        System.out.println("今年的第 " + calendar.get(Calendar.DAY_OF_YEAR) + "天");

        // 本月第 N 天
        System.out.println("本月的第 " + calendar.get(Calendar.DAY_OF_MONTH) + "天");

        // 3小时以后
        calendar.add(Calendar.HOUR_OF_DAY, 3);
        System.out.println("三小时以后的时间： " + calendar.getTime());
        // 格式化显示
        str = (new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SS")).format(calendar.getTime());
        System.out.println(str);

        // 重置 Calendar 显示当前时间
        calendar.setTime(new Date());
        str = (new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SS")).format(calendar.getTime());
        System.out.println(str);

        // 创建一个 Calendar 用于比较时间
        Calendar calendarNew = Calendar.getInstance();

        // 设定为 5 小时以前，后者大，显示 -1
        calendarNew.add(Calendar.HOUR, -5);
        System.out.println("时间比较：" + calendarNew.compareTo(calendar));

        // 设定7小时以后，前者大，显示 1
        calendarNew.add(Calendar.HOUR, +7);
        System.out.println("时间比较：" + calendarNew.compareTo(calendar));

        // 退回 2 小时，时间相同，显示0
        calendarNew.add(Calendar.HOUR, -2);
        System.out.println("时间比较：" + calendarNew.compareTo(calendar));

        // calendarNew创建时间点
        System.out.println((new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SS")).format(calendarNew.getTime()));
        // calendar创建时间点
        System.out.println((new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SS")).format(calendar.getTime()));
        System.out.println("时间比较：" + calendarNew.compareTo(calendar));
    }
}
```

编译运行：
``` java
$ javac CalendarDemo.java
$ java CalendarDemo
完整显示日期时间：
2018-12-12 15:50:49
年： 2018
月： 11  // 0 代表 1 月，11 代表 12 月
分钟： 50
今年的第 346天
本月的第 12天
三小时以后的时间： Wed Dec 12 18:50:49 CST 2018
2018-12-12 18:50:49:449
2018-12-12 15:50:49:455
时间比较：-1
时间比较：1
时间比较：1
2018-12-12 15:50:49:456
2018-12-12 15:50:49:455
时间比较：1
```

最后一个的输出为什么有时是 0 ，有时是 1，在这里会涉及到 calendarNew 与 calendar 的创建时间点， calendarNew 经过增加和减少时间后恢复到原来的时间点，也就是最终比较的是谁先创建好，时间点靠后的大一些，而 calendarNew 创建的时间点只有可能是大于等于 calendar 的，需要根据实际的创建时间点进行比较。

#### Date
Date 类表示日期和时间，里面封装了操作日期和时间的方法。Date 类经常用来获取系统当前时间。

Date 中定义的未过时的构造方法：  

| 构造方法            | 说明                                                          |
|-----------------|-------------------------------------------------------------|
| Date()          | 构造一个 Date 对象并对其进行初始化以反映当前时间                                 |
| Date(long date) | 构造一个 Date 对象，并根据相对于 GMT 1970 年 1 月 1 日 00:00:00 的毫秒数对其进行初始化 |

Date编程示例：
``` java
import java.text.SimpleDateFormat;
import java.util.Date;

public class DateDemo {
    public static void main(String[] args) {
        String strDate, strTime;
        Date objDate = new Date();
        System.out.println("今天的日期是：" + objDate);
        long time = objDate.getTime();
        System.out.println("自1970年1月1日起以毫秒为单位的时间（GMT）：" + time);
        strDate = objDate.toString();
        //提取 GMT 时间
        strTime = strDate.substring(11, (strDate.length() - 4));
        //按小时、分钟和秒提取时间
        strTime = "时间：" + strTime.substring(0, 8);
        System.out.println(strTime);
        //格式化时间
        SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        System.out.println(formatter.format(objDate));
    }
}
```

编译运行：  
``` java
$ javac DateDemo.java
$ java DateDemo
今天的日期是：Wed Dec 12 14:43:15 CST 2018
自1970年1月1日起以毫秒为单位的时间（GMT）：1544596995669
时间：14:43:15
2018-12-12 14:43:15
```

Date 类的很多方法自 JDK 1.1 开始就已经过时了。

#### Math
Math 类在 java.lang 包中，包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。

常见方法： 

| 方法                      | 返回值                                   | 功能描述                                                   |
|-------------------------|---------------------------------------|--------------------------------------------------------|
| sin(double numvalue)    | double                                | 计算角 numvalue 的正弦值                                      |
| cos(double numvalue)    | double                                | 计算角 numvalue 的余弦值                                      |
| acos(double numvalue)   | double                                | 计算 numvalue 的反余弦                                       |
| asin(double numvalue)   | double                                | 计算 numvalue 的反正弦                                       |
| atan(double numvalue)   | double                                | 计算 numvalue 的反正切                                       |
| pow(double a, double b) | double                                | 计算 a 的 b 次方                                            |
| sqrt(double numvalue)   | double                                | 计算给定值的正平方根                                             |
| abs(int numvalue)       | int                                   | 计算 int 类型值 numvalue 的绝对值，也接收 long、float 和 double 类型的参数 |
| ceil(double numvalue)   | double                                | 返回大于等于 numvalue 的最小整数值                                 |
| floor(double numvalue)  | double                                | 返回小于等于 numvalue 的最大整数值                                 |
| max(int a, int b)       | int                                   | 返回 int 型 a 和 b 中的较大值，也接收 long、float 和 double 类型的参数     |
| min(int a, int b)       | int                                   | 返回 a 和 b 中的较小值，也可接受 long、float 和 double 类型的参数          |
| rint(double numvalue)   | double                                | 返回最接近 numvalue 的整数值                                    |
| round(T arg)            | arg 为 double 时返回 long，为 float 时返回 int | 返回最接近arg的整数值                                           |
| random()                | double                                | 返回带正号的 double 值，该值大于等于 0.0 且小于 1.0                     |

Math编程示例：
``` java
public class MathDemo {
    public static void main(String[] args) {
        System.out.println(Math.abs(-12.7));
        System.out.println(Math.ceil(12.7));
        System.out.println(Math.rint(12.4));
        System.out.println(Math.random());
        System.out.println("sin30 = " + Math.sin(Math.PI / 6));
        // 计算30°的正弦值，参数是用弧度表示的角，即π的六分之一
        System.out.println("cos30 = " + Math.cos(Math.PI / 6));
        // 计算30°的余弦值，这些计算三角函数的方法，其参数和返回值的类型都为double
        System.out.println("tan30 = " + Math.tan(Math.PI / 6));
        // 计算30°的正切值
    }
}
```

编译运行：  
``` bash
$ javac MathDemo.java
$ java MathDemo
12.7
13.0
12.0
0.8011998172263968
sin30 = 0.49999999999999994
cos30 = 0.8660254037844387
tan30 = 0.5773502691896257
```

#### System
System 类提供了一下功能：
1. 标准输入，标准输出和错误输出流;
2. 访问外部定义的属性和环境变量;
3. 加载文件和库的方法;
4. 以及用于快速复制数组的实用方法。

System 不可以被实例化，只可以使用其静态方法。

``` java
//从指定的源数组中复制一个数组，从源数组指定的位置开始，到目标数组指定的位置
public static void arraycopy(Object src,int srcPos, Object dest,int desPos,int length) 
//返回以毫秒为单位的当前时间(从1970年到现在的毫秒数)
public static long currentTimeMillis()  
//终止当前正在运行的Java虚拟机，status为 0时退出
public static void exit(int status)  
//  运行垃圾收集器
public static void gc() 
// 取得当前系统的全部属性
public static Properties getProperties()
//获取指定键的系统属性
public static String  getProperty(String key) 
```

System编程示例：  
``` java
import java.util.Arrays;

public class SystemDemo {
    public static void main(String[] args) {
        int[] a = {7, 8, 9, 10, 11};
        int[] b = {1, 2, 3, 4, 5, 6};
        //从数组a的第二个元素开始，复制到b数组的第三个位置 复制的元素长度为3
        System.arraycopy(a, 1, b, 2, 3);
        //输出结果
        System.out.println(Arrays.toString(b));
        System.out.println("当前时间：" + System.currentTimeMillis());
        System.out.println("java版本信息：" + System.getProperty("java.version"));
        //运行垃圾收集器
        System.gc();
        //退出
        System.exit(0);
    }
}
```

编译运行：
``` bash
$ javac SystemDemo.java
$ java SystemDemo
[1, 2, 8, 9, 10, 6]
当前时间：1544670501472
java版本信息：11
``` 

#### Random
Random 类用于生成伪随机数流，在java.util包下。  

Random编程示例：  
``` java
import java.util.Random;

public class RandomDemo {
    public static void main(String[] args) {
        Random random = new Random();
        //随机生成一个整数 int范围
        System.out.println(random.nextInt());
        //生成 [0,n] 范围的整数  设n=100
        System.out.println(random.nextInt(100 + 1));
        //生成 [0,n) 范围的整数  设n=100
        System.out.println(random.nextInt(100));
        //生成 [m,n] 范围的整数  设n=100 m=40
        System.out.println((random.nextInt(100 - 40 + 1) + 40));
        //随机生成一个整数 long范围
        System.out.print(random.nextLong());
        //生成[0,1.0)范围的float型小数
        System.out.println(random.nextFloat());
        //生成[0,1.0)范围的double型小数
        System.out.println(random.nextDouble());
    }
}
```

编译运行：
``` bash
$ javac RandomDemo.java
$ java RandomDemo
272128541
67
93
66
-23177167376469717070.93104035
0.20044632645967309
```


### 泛型和集合
- 泛型
- Collection
- List
- ArrayList
- Map
- HashMap
- Set 和 HashSet
- Collections
- 算法

#### 泛型 -todo
泛型即参数化类型，也就是说数据类型变成了一个可变的参数，在不使用泛型的情况下，参数的数据类型都是写死了的，使用泛型之后，可以根据程序的需要进行改变。

定义泛型的规则：

1. 只能是类类型，不能是简单数据类型
1. 泛型参数可以有多个
1. 可以用使用 extends 语句或者 super 语句 如<T extends superClass>表示类型的上界，T 只能是 superClass 或其子类， <K super childClass>表示类型的下界，K 只能是 childClass 或其父类。
1. 可以是通配符类型，比如常见的 Class<?>

定义泛型示例：  
``` java
/*
使用T代表类型，无论何时都没有比这更具体的类型来区分它。如果有多个类型参数，我们可能使用字母表中T的临近的字母，比如S。
*/
class Test<T> {
    private T ob;

    /*
    定义泛型成员变量，定义完类型参数后，可以在定义位置之后的方法的任意地方使用类型参数，就像使用普通的类型一样。
    注意，父类定义的类型参数不能被子类继承。
    */

    //构造函数
    public Test(T ob) {
        this.ob = ob;
    }

    //getter 方法
    public T getOb() {
        return ob;
    }


    //setter 方法
    public void setOb(T ob) {
        this.ob = ob;
    }

    public void showType() {
        System.out.println("T的实际类型是: " + ob.getClass().getName());
    }
}

public class TestDemo {
    public static void main(String[] args) {
        // 定义泛型类 Test 的一个Integer版本
        Test<Integer> intOb = new Test<Integer>(88);
        intOb.showType();
        int i = intOb.getOb();
        System.out.println("value= " + i);
        System.out.println("----------------------------------");
        // 定义泛型类Test的一个String版本
        Test<String> strOb = new Test<String>("Hello Gen!");
        strOb.showType();
        String s = strOb.getOb();
        System.out.println("value= " + s);
    }
}
```

编译运行：  
``` bash
$ javac TestDemo.java
$ java TestDemo
T的实际类型是: java.lang.Integer
value= 88
----------------------------------
T的实际类型是: java.lang.String
value= Hello Gen!
```

#### Collection
集合框架是为表示和操作集合而规定的一种统一的标准的体系结构。任何集合框架都包含三大内容：对外的接口、接口的实现和对集合运算的算法。

下图是简化的集合框架关系图：
![](https://raw.githubusercontent.com/huahuayu/img/master/20190628171530.png)

因为集合框架中的很多类功能是相似的，所以我们用接口来规范类。Collection 接口是 java 集合框架里的一个根接口。它也是 List、Set 和 Queue 接口的父接口。Collection 接口中定义了可用于操作 List、Set 和 Queue 的方法——增删改查。

| 方法                               | 返回值         | 说明                                                |
|----------------------------------|-------------|---------------------------------------------------|
| add(E e)                         | boolean     | 向 collection 的尾部追加指定的元素（可选操作）                     |
| addAll(Collection<? extend E> c) | boolean     | 将指定 collection 中的所有元素都添加到此 collection 中（可选操作）     |
| clear()                          | void        | 移除此 collection 中的所有元素（可选操作）                       |
| contains(Object o)               | boolean     | 如果此 collection 包含指定的元素，则返回 true                   |
| containsAll(Collection<?> c)     | boolean     | 如果此 collection 包含指定 collection 的所有元素，则返回 true     |
| equals(Object o)                 | boolean     | 比较此 collection 与指定对象是否相等                          |
| hashCode()                       | int         | 返回此 collection 的哈希码值                              |
| isEmpty()                        | boolean     | 如果此 collection 不包含元素，则返回true                      |
| iterator()                       | Iterator<E> | 返回在此 collection 的元素上进行迭代的迭代器                      |
| remove(Object o)                 | boolean     | 移除此 collection 中出现的首个指定元素(可选操作)                   |
| removeAll(Collection<?> c)       | boolean     | 移除此 collection 中那些也包含在指定 collection 中的所有元素（可选操作）  |
| retainAll(Collection<?> c)       | boolean     | 仅保留此 collection 中那些也包含在指定 collection 的元素（可选操作）    |
| size()                           | int         | 返回此 collection 中的元素数                              |
| toArray()                        | Object[]    | 返回包含此 collection 中所有元素的数组                         |
| toArray(T[] a)                   | <T> T[]     | 返回包含此 collection 中所有元素的数组；返回数组的运行时类型与指定数组的运行时类型相同 |

#### List
`List` 是一个接口，不能实例化，需要一个具体类来实现实例化。List 集合中的对象按照一定的顺序排放，里面的内容可以重复。 List 接口实现的类有：`ArrayList`（实现动态数组），`Vector`（实现动态数组），`LinkedList`（实现链表），`Stack`（实现堆栈）。

List 在 Collection 基础上增加的方法：

| 方法                                           | 返回值             | 说明                                           |
|----------------------------------------------|-----------------|----------------------------------------------|
| add(int index, E element)                    | void            | 在列表的指定位置插入指定元素（可选操作）                         |
| addAll(int index, Collection<? extends E> c) | boolean         | 将指定 collection 中的所有元素都插入到列表中的指定位置（可选操作）      |
| get(int index)                               | E               | 返回列表中指定位置的元素                                 |
| indexOf(Object o)                            | int             | 返回此列表中第一次出现的指定元素的索引；如果此列表不包含该元素，则返回 -1       |
| lastIndexOf(Object o)                        | int             | 返回此列表中最后出现的指定元素的索引；如果列表不包含此元素，则返回 -1         |
| listIterator()                               | ListIterator<E> | 返回此列表元素的列表迭代器（按适当顺序）                         |
| listIterator(int index)                      | ListIterator<E> | 返回此列表元素的列表迭代器（按适当顺序），从列表的指定位置开始              |
| remove(int index)                            | E               | 移除列表中指定位置的元素（可选操作）                           |
| set(int index, E element)                    | E               | 用指定元素替换列表中指定位置的元素（可选操作）                      |
| subList(int fromIndex, int toIndex)          | List<E>         | 返回列表中指定的 fromIndex（包括 ）和 toIndex（不包括）之间的部分视图 |

#### ArrayList
ArrayList　类实现一个可增长的动态数组，位于 java.util.ArrayList<E>。实现了 List 接口，它可以存储不同类型的对象（包括 null 在内），而数组则只能存放特定数据类型的值。

ArrayList 编程实例
学校的教务系统会对学生进行统一的管理，每一个学生都会有一个学号和学生姓名，我们在维护整个系统的时候，大多数操作是对学生的添加、插入、删除、修改等操作。

#### Map
Map 接口也是一个非常重要的集合接口，用于存储键/值对。Map 中的元素都是成对出现的，键值对就像数组的索引与数组的内容的关系一样，将一个键映射到一个值的对象。一个映射不能包含重复的键；每个键最多只能映射到一个值。我们可以通过键去找到相应的值。

value 可以存储任意类型的对象，我们可以根据 key 键快速查找 value。Map 中的键/值对以 Entry 类型的对象实例形式存在。

| 方法                                      | 返回值                 | 说明                                  |
|-----------------------------------------|---------------------|-------------------------------------|
| clear()                                 | void                | 从此映射中移除所用映射关系（可选操作）                 |
| containsKey(Object key)                 | boolean             | 如果此映射包含指定键的映射关系，则返回true             |
| containsValue(Object value)             | boolean             | 如果此映射将一个或多个键映射到指定值，则返回 true         |
| entrySet()                              | Set<Map.Entry<K,V>> | 返回此映射中包含的映射关系的 Set 视图               |
| equals(Object o)                        | boolean             | 比较指定的对象与此映射是否相等                     |
| get(Object key)                         | V                   | 返回指定键所映射的值；如果此映射不包含该键的映射关系，则返回 null |
| hashCode()                              | int                 | 返回此映射的哈希码值                          |
| isEmpty()                               | boolean             | 如果此映射未包含键-值映射关系，则返回 true            |
| keySet()                                | Set<K>              | 返回此映射中包含的键的 Set 视图                  |
| put(K key, V value)                     | V                   | 将指定的值与此映射中的指定键关联（可选操作）              |
| putAll(Map<? extends K, ? extends V> m) | void                | 从指定映射中将所有映射关系复制到此映射中（可选操作）          |
| remove(Object key)                      | V                   | 如果存在一个键的映射关系，则将其从此映射中移除（可选操作）       |
| size                                    | int                 | 返回此映射中的键-值映射关系数                     |
| values()                                | Collection<V>       | 返回此映射中包含的值的 Collection 视图           |

#### HashMap
HashMap 是基于哈希表的 Map 接口的一个重要实现类。HashMap 中的 Entry 对象是无序排列的，Key 值和 value 值都可以为 null，但是一个 HashMap 只能有一个 key 值为 null 的映射（key 值不可重复）。

下面我们通过代码来学习 Map 中的方法吧。同学们都有过选课经历吧，我们就用 Map 来管理课程吧。

#### Set 和 HashSet
Set 接口也是 Collection 接口的子接口，它有一个很重要也是很常用的实现类——HashSet，Set 是元素无序并且不包含重复元素的 collection（List 可以重复），被称为集。

HashSet 由哈希表（实际上是一个 HashMap 实例）支持。它不保证 set 的迭代顺序；特别是它不保证该顺序恒久不变。

#### Collections
java.util.Collections 是一个工具类，他包含了大量对集合进行操作的静态方法。  
常用方法：  

| 方法名                                                         | 描述                       |
|-------------------------------------------------------------|--------------------------|
| void sort(List list)                                        | 按自然升序排序                  |
| void sort(List list, Comparator c)                          | 自定义排序规则排序                |
| void shuffle(List list)                                     | 随机排序，用于打乱顺序              |
| void reverse(List list)                                     | 反转，将列表元素顺序反转             |
| void swap(List list, int i , int j)                         | 交换处于索引 i 和 j 位置的元素       |
| int binarySearch(List list, Object key)                     | 二分查找，列表必须有序，返回找到的元素索引位置  |
| int max(Collection coll)                                    | 查找最大值                    |
| int min(Collection coll)                                    | 查找最小值                    |
| void fill(List list, Object obj)                            | 使用 obj 填充 list 所有元素      |
| boolean replaceAll(List list, Object oldVal, Object newVal) | 使用用 newVal 替换所有的 oldVal。 |
| <K,V> Map<K,V> synchronizedMap(Map<K,V> m)                  | 将 m 包装为线程安全的 Map         |
| <T> List<T> synchronizedList(List<T> list)                  | 将 list 包装为线程安全的 List     |

程序示例：
``` javaimport java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsDemo {
    public static void main(String[] args) {
//        创建一个空List
        List<Integer> list = new ArrayList<>();
        //赋值
        list.add(3);
        list.add(5);
        list.add(7);
        list.add(9);
        list.add(12);
        System.out.print("初始顺序：");
        list.forEach(v -> System.out.print(v + "\t"));


        //打乱顺序
        Collections.shuffle(list);
        System.out.print("\n打乱顺序：");
        list.forEach(v -> System.out.print(v + "\t"));

        //反转
        Collections.reverse(list);
        System.out.print("\n反转集合：");
        list.forEach(v -> System.out.print(v + "\t"));

        //第一个位和最后一位交换
        Collections.swap(list,0,list.size()-1);
        System.out.print("\n交换第一位和最后一位：");
        list.forEach(v -> System.out.print(v + "\t"));

        //按自然升序排序
        Collections.sort(list);
        System.out.print("\nSort排序后：");
        list.forEach(v -> System.out.print(v + "\t"));

        //二分查找 必须排序后
        System.out.print("\n二分查找数值7的位置："+Collections.binarySearch(list, 7));

        //返回线程安全的list
        List<Integer> synchronizedList = Collections.synchronizedList(list);
    }
}
```

编译运行：
``` bash
$ javac CollectionsDemo.java
$ java CollectionsDemo
初始顺序：3    5    7    9    12    
打乱顺序：5    7    3    12    9    
反转集合：9    12    3    7    5    
交换第一位和最后一位：5    12    3    7    9    
Sort排序后：3    5    7    9    12    
二分查找数值7的位置：2
```

### 算法
#### 插入排序
``` java
import java.util.Arrays;

public class InsertSort {
    public static void sort(int[] arr) {
        int temp;
        for (int i = 1; i < arr.length; i++) {
            for (int j = 0; j < i; j++) {
                //对已经排序好的元素比较，找到一个比插入元素大的元素 交换位置
                if (arr[i] < arr[j]) {
                    temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] ints = {5, 3, 4, 1, 2};
        sort(ints);
        System.out.println(Arrays.toString(ints));
    }
}
```

#### 冒泡排序
``` java
import java.util.Arrays;

public class BubbleSort {
    public static void sort(int[] arr) {
        for (int i = 0; i < arr.length-1; i++) {
            for (int j = 0; j < arr.length - i - 1; j++) {
                //如果当前元素比后一位元素大 交换位置
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    public static void main(String[] args) {
        int[] ints = {5, 3, 4, 1, 2};
        sort(ints);
        System.out.println(Arrays.toString(ints));
    }
}
```

#### 归并排序
``` java
import java.util.Arrays;

public class MergeSort {

    public static void mergeSort(int[] arrays, int left, int right) {
//        如果数组还可以拆分
        if (left < right) {
            //数组的中间位置
            int middle = (left + right) / 2;
            //拆分左边数组
            mergeSort(arrays, left, middle);
            //拆分右边数组
            mergeSort(arrays, middle + 1, right);
            //合并
            merge(arrays, left, middle, right);

        }
    }


    /**
     * 合并数组
     */
    public static void merge(int[] arr, int left, int middle, int right) {
        //申请合并空间 大小为两个已经排序序列之和
        int[] temp = new int[right - left + 1];
        //i 和 j为两个已经排好序的数组的起始位置
        int i = left;
        int j = middle + 1;
        int k = 0;
        //排序
        while (i <= middle && j <= right) {
            //将比较小的数组放入合并空间
            if (arr[i] < arr[j]) {
                temp[k++] = arr[i++];
            } else {
                temp[k++] = arr[j++];
            }
        }
        //将左边剩余元素写入合并空间
        while (i <= middle) {
            temp[k++] = arr[i++];
        }
        //将右边剩余的元素写入合并空间
        while (j <= right) {
            temp[k++] = arr[j++];
        }
        //将排序后的数组写回原来的数组
        for (int l = 0; l < temp.length; l++) {
            arr[l + left] = temp[l];
        }

    }

    public static void main(String[] args) {
        int[] ints = {5, 3, 4, 1, 2};
        mergeSort(ints,0,ints.length-1);
        System.out.println(Arrays.toString(ints));
    }
}
```

#### 快速排序
``` java
import java.util.Arrays;

public class QuickSort {
    public static void sort(int[] arr, int head, int tail) {
        if (head >= tail || arr == null || arr.length <= 1) {
            return;
        }
        //设置数组的起始位置 i 结束位置j 基准 pivot 为数组的中间
        int i = head, j = tail, pivot = arr[(head + tail) / 2];
        while (i <= j) {
            //当数组小于基准 循环结束后 相当于i所处的位置的值为大于基准的元素
            while (arr[i] < pivot) {
                ++i;
            }
            //当数组大于基准 循环结束后 相当于j所处的位置的值为小于于基准的元素
            while (arr[j] > pivot) {
                --j;
            }
            //如果i<j 那么则将交互i j对应位置的值
            if (i < j) {
                int t = arr[i];
                arr[i] = arr[j];
                arr[j] = t;
                //将指针继续移动
                ++i;
                --j;
            } else if (i == j) {
//如果i=j 那么说明本次排序已经结束 将i++ 如果这里不使用i++ 那么后面的sort(arr,i,tail)将改为arr(arr,i+1,tail)
                ++i;
            }
        }
        //继续将数组分割  
        sort(arr, head, j);
        sort(arr, i, tail);
    }

    public static void main(String[] args) {
        int[] ints = {5, 3, 4, 1, 2};
        sort(ints, 0, ints.length - 1);
        System.out.println(Arrays.toString(ints));
    }
}
```

#### 线性搜索
``` java
public class LinearSearch {
    public static void main(String[] args) {
        int[] ints = {5, 3, 4, 1, 2};
        System.out.println(search(ints, 4));
    }

    public static int search(int[] arr, int key) {
        //循环
        for (int i = 0; i < arr.length; i++) {
            //比较是否等于key
            if (arr[i] == key) {
                return arr[i];
            }
        }
        //找不到就返回-1
        return -1;
    }
}
```

#### 二分查找
``` java
public class BinarySearch {
    public static int search(int[] arr, int key) {
        int low = 0;
        int high = arr.length - 1;
        while (low <= high) {
            int middle = (high + low) / 2;
            //如果相等 返回值
            if (key == arr[middle]) {
                return key;
            } else if (key < arr[middle]) {
                //如果key小于中间值，那么改变high，值可能在左边部（比较小的部分）
                high = middle - 1;
            }else {
                //如果key大于中间值，那么改变low，值可能在右边部（比较大的部分）
                low = middle + 1;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] ints = {5, 3, 4, 1, 2};
        System.out.println(search(ints, 4));
    }
}
```

### 异常
异常指不期而至的各种状况，它在程序运行的过程中发生。作为开发者，我们都希望自己写的代码永远都不会出现bug，然而现实告诉我们并没有这样的情景。如果用户在程序的使用过程中因为一些原因造成他的数据丢失，这个用户就可能不会再使用该程序了。所以，对于程序的错误以及外部环境能够对用户造成的影响，我们应当及时报告并且以适当的方式来处理这个错误。

之所以要处理异常，也是为了增强程序的鲁棒性。

异常都是从Throwable类派生出来的，而Throwable类是直接从Object类继承而来。

#### 异常分类
异常通常有四类：

1. Error：系统内部错误，这类错误由系统进行处理，程序本身无需捕获处理
1. Exception：可以处理的异常
1. RuntimeException：可以捕获，也可以不捕获的异常
1. 继承 Exception 的其他类：必须捕获，通常在 API 文档中会说明这些方法抛出哪些异常

平时主要关注的异常是 Exception 下的异常，而 Exception 异常下又主要分为两大类异常，一个是派生于 RuntimeExcption 的异常，一个是除了 RuntimeExcption 体系之外的其他异常。

RuntimeExcption 异常(运行时异常)通常有以下几种：

1. 错误的类型转换
1. 数组访问越界
1. 访问 null 指针
1. 算术异常

一般来说，RuntimeException 都是程序员的问题。

非 RuntimeException（受查异常）一般有：

1. 打开一个不存在的文件
1. 没有找到具有指定名称的类
1. 操作文件异常

受查异常是编译器要求必须处理的异常，必须使用 try catch 处理，或者向上抛出，给上层处理。

#### 声明及抛出
**throw 抛出异常**   
当程序运行时数据出现错误或者我们不希望发生的情况出现的话，可以通过抛出异常来处理。

异常抛出语法：
``` java
throw new 异常名();
```

程序示例：  
``` java
public class ThrowTest {

    public static void main(String[] args) {
        Integer a = 1;
        Integer b = null;
        //当a或者b为null时，抛出异常
        if (a == null || b == null) {
            throw new NullPointerException();
        } else {
            System.out.println(a + b);
        }
    }
}
```
```
$ javac ThrowTest.java
$ java ThrowTest
Exception in thread "main" java.lang.NullPointerException
    at ThrowTest.main(ThrowTest.java:8)
```

**throws 声明异常**
``` java
import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class ThrowsTest {

    public static void main(String[] args) throws FileNotFoundException {
        //由方法的调用者捕获异常或者继续向上抛出
        throwsTest();

    }

    public static void throwsTest() throws FileNotFoundException {
        new FileInputStream("/home/project/shiyanlou.file");
    }
}
```

``` bash$ javac ThrowsTest.java
$ java ThrowsTest
Exception in thread "main" java.io.FileNotFoundException: /home/project/shiyanlou.file (系统找不到指定的路径。)
    at java.io.FileInputStream.open0(Native Method)
    at java.io.FileInputStream.open(FileInputStream.java:195)
    at java.io.FileInputStream.<init>(FileInputStream.java:138)
    at java.io.FileInputStream.<init>(FileInputStream.java:93)
    at ThrowsTest.throwsTest(ThrowsTest.java:13)
    at ThrowsTest.main(ThrowsTest.java:8)
```

#### 捕获异常
通常抛出异常后，还需要将异常捕获。使用try和catch语句块来捕获异常，有时候还会用到finally。

对于上述三个关键词所构成的语句块，try语句块是必不可少的，catch和finally语句块可以根据情况选择其一或者全选。你可以把可能发生错误或出现问题的语句放到try语句块中，将异常发生后要执行的语句放到catch语句块中，而finally语句块里面放置的语句，不管异常是否发生，它们都会被执行。

你可能想说，那我把所有有关的代码都放到try语句块中不就妥当了吗？可是你需要知道，捕获异常对于系统而言，其开销非常大，所以应尽量减少该语句块中放置的语句。

编程示例：  
``` java
public class CatchException {
    public static void main(String[] args) {
        try {
            // 下面定义了一个try语句块

            System.out.println("I am try block.");

            Class<?> tempClass = Class.forName("");    
            // 声明一个空的Class对象用于引发“类未发现异常”
            System.out.println("Bye! Try block.");

        } catch (ClassNotFoundException e) {
            // 下面定义了一个catch语句块
            System.out.println("I am catch block.");

            e.printStackTrace();
            //printStackTrace()的意义在于在命令行打印异常信息在程序中出错的位置及原因

            System.out.println("Goodbye! Catch block.");

        } finally {
            // 下面定义了一个finally语句块
            System.out.println("I am finally block.");
        }
    }
}
``` 

``` bash
$ javac CatchException.java
$ java CatchException
I am try block.
I am catch block.
java.lang.ClassNotFoundException:
        at java.lang.Class.forName0(Native Method)
        at java.lang.Class.forName(Unknown Source)
        at CatchException.main(CatchException.java:8)
Goodbye! Catch block.
I am finally block.
```

#### 捕获多个异常
在一段代码中，可能会由于各种原因抛出多种不同的异常，而对于不同的异常，我们希望用不同的方式来处理它们，而不是笼统的使用同一个方式处理，在这种情况下，可以使用异常匹配，当匹配到对应的异常后，后面的异常将不再进行匹配。

编程示例：  
``` java
import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class MultipleCapturesDemo {
    public static void main(String[] args) {
        try {
            new FileInputStream("");
        } catch (FileNotFoundException e) {
            System.out.println("IO 异常");
        } catch (Exception e) {
            System.out.println("发生异常");
        }
    }
}
```

``` bash
$ javac MultipleCapturesDemo.java
$ java MultipleCapturesDemo
IO 异常
```

在处理异常时，并不要求抛出的异常同 catch 所声明的异常完全匹配，子类的对象也可以匹配父类的处理程序。比如异常 A 继承于异常 B，那么在处理多个异常时，一定要将异常 A 放在异常 B 之前捕获，如果将异常 B 放在异常 A 之前，那么将永远匹配到异常 B，异常 A 将永远不可能执行，并且编译器将会报错。

#### 自定义异常
尽管 Java SE 的 API 已经为我们提供了数十种异常类，然而在实际的开发过程中，你仍然可能遇到未知的异常情况。此时，你就需要对异常类进行自定义。

自定义一个异常类非常简单，只需要让它继承 Exception 或其子类就行。在自定义异常类的时候，建议同时提供无参构造方法和带字符串参数的构造方法，后者可以为你在调试时提供更加详细的信息。

自定义异常：  
``` java
// MyAriException.java
public class MyAriException extends ArithmeticException {
    //自定义异常类，该类继承自ArithmeticException

    public MyAriException() {

    }
    //实现默认的无参构造方法

    public MyAriException(String msg) {
        super(msg);
    }
    //实现可以自定义输出信息的构造方法，将待输出信息作为参数传入即可
}
```

测试自定义异常：  
``` java
// ExceptionTest.java
import java.util.Arrays;

public class ExceptionTest {
    public static void main(String[] args) {
        int[] array = new int[5];
        //声明一个长度为5的数组

        Arrays.fill(array, 5);
        //将数组中的所有元素赋值为5

        for (int i = 4; i > -1; i--) {
            //使用for循环逆序遍历整个数组，i每次递减

            if (i == 0) {
            // 如果i除以了0，就使用带异常信息的构造方法抛出异常

                throw new MyAriException("There is an exception occured.");
            }

            System.out.println("array[" + i + "] / " + i + " = " + array[i] / i);
            // 如果i没有除以0，就输出此结果
        }
    }
}
```

``` bash
$ javac ExceptionTest.java MyAriException.java
$ java ExceptionTest
array[4] / 4 = 1
array[3] / 3 = 1
array[2] / 2 = 2
array[1] / 1 = 5
Exception in thread "main" MyAriException: There is an exception occured.
    at ExceptionTest.main(ExceptionTest.java:17)
```

#### 异常堆栈
 当异常抛出后，我们可以通过异常堆栈追踪程序的运行轨迹，以便我们更好的DEBUG。

 编程示例：  
 ``` java
 public class ExceptionStackTrace {
    private static void method1() {
        method2();
    }

    private static void method2() {
        throw new NullPointerException();
    }
    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            //打印堆栈轨迹
            e.printStackTrace();
        }
    }
}
```
```
$ javac ExceptionStackTrace.java
$ java ExceptionStackTrace
java.lang.NullPointerException
    at ExceptionStackTrace.method2(ExceptionStackTrace.java:7)
    at ExceptionStackTrace.method1(ExceptionStackTrace.java:3)
    at ExceptionStackTrace.main(ExceptionStackTrace.java:11)
```

通过上面的异常堆栈轨迹，在对比我们方法的调用过程，可以得出异常信息中首先打印的是距离抛出异常最近的语句，接着是调用该方法的方法，一直到最开始被调用的方法。从下往上看，就可以得出程序运行的轨迹。

### Lambda表达式
Lambda 表达式是 Java SE 8 中一个重要的新特性。Lambda 表达式允许你通过表达式来代替功能接口。

#### 函数式编程
函数式编程（英语：functional programming）或称函数程序设计，又称泛函编程，是一种编程典范，它将计算机运算视为数学上的函数计算，并且避免使用程序状态以及易变对象。函数编程语言最重要的基础是λ演算（lambda calculus）。而且λ演算的函数可以接受函数当作输入（引数）和输出（传出值）。

#### Lambda表达式
一个 Lambda 表达式具有下面这样的语法特征。它由三个部分组成：第一部分为一个括号内用逗号分隔的参数列表，参数即函数式接口里面方法的参数；第二部分为一个箭头符号：->；第三部分为方法体，可以是表达式和代码块。语法如下：

```
parameter -> expression body
```

下面列举了 Lambda 表达式的几个最重要的特征：

1. 可选的类型声明：你不用去声明参数的类型。编译器可以从参数的值来推断它是什么类型。
1. 可选的参数周围的括号：你可以不用在括号内声明单个参数。但是对于很多参数的情况，括号是必需的。
1. 可选的大括号：如果表达式体里面只有一个语句，那么你不必用大括号括起来。
1. 可选的返回关键字：如果表达式体只有单个表达式用于值的返回，那么编译器会自动完成这一步。若要指示表达式来返回某个值，则需要使用大括号。

编程示例：  
``` java
public class LamdbaTest {
    public static void main(String args[]){
        LamdbaTest tester = new LamdbaTest();

          // 带有类型声明的表达式
          MathOperation addition = (int a, int b) -> a + b;

          // 没有类型声明的表达式
          MathOperation subtraction = (a, b) -> a - b;

          // 带有大括号、带有返回语句的表达式
          MathOperation multiplication = (int a, int b) -> { return a * b; };

          // 没有大括号和return语句的表达式
          MathOperation division = (int a, int b) -> a / b;

          // 输出结果
          System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
          System.out.println("10 - 5 = " + tester.operate(10, 5, subtraction));
          System.out.println("10 x 5 = " + tester.operate(10, 5, multiplication));
          System.out.println("10 / 5 = " + tester.operate(10, 5, division));

          // 没有括号的表达式            
          GreetingService greetService1 = message ->
          System.out.println("Hello " + message);

          // 有括号的表达式            
          GreetingService greetService2 = (message) ->
          System.out.println("Hello " + message);

          // 调用sayMessage方法输出结果
          greetService1.sayMessage("Shiyanlou");
          greetService2.sayMessage("Classmate");
       }

       // 下面是定义的一些接口和方法

       interface MathOperation {
          int operation(int a, int b);
       }

       interface GreetingService {
          void sayMessage(String message);
       }

       private int operate(int a, int b, MathOperation mathOperation){
          return mathOperation.operation(a, b);
       }
}
```

```
$ javac LamdbaTest.java
$ java LamdbaTest
10 + 5 = 15
10 - 5 = 5
10 x 5 = 50
10 / 5 = 2 
Hello Shiyanlou
Hello Classmate
```

需要注意的是：

1. Lambda 表达式优先用于定义功能接口在行内的实现，即单个方法只有一个接口。在上面的例子中，我们用了多个类型的 Lambda 表达式来定义 MathOperation 接口的操作方法。然后我们定义了 GreetingService 的 sayMessage 的实现。
1. Lambda 表达式让匿名类不再需要，这为 Java 增添了简洁但实用的函数式编程能力。


#### Lambda作用域
``` java
public class LamdbaTest {
        final static String salutation = "Hello "; //正确，不可再次赋值
        //static String salutation = "Hello "; //正确，可再次赋值
        //String salutation = "Hello "; //报错
        //final String salutation = "Hello "; //报错

    public static void main(String args[]){
        //final String salutation = "Hello "; //正确，不可再次赋值
        //String salutation = "Hello "; //正确，隐性为 final , 不可再次赋值

        // salution = "welcome to "  
        GreetingService greetService1 = message -> 
        System.out.println(salutation + message);
        greetService1.sayMessage("Shiyanlou");
    }

    interface GreetingService {
       void sayMessage(String message);
    }
}
```

``` bash
$ javac LamdbaTest.java
$ java LamdbaTest
Hello Shiyanlou
```

可以得到以下结论：

1. 可访问 static 修饰的成员变量，如果是 final static 修饰，不可再次赋值，只有 static 修饰可再次赋值；
2. 可访问表达式外层的 final 局部变量（不用声明为 final，隐性具有 final 语义），不可再次赋值。


## maven
### maven helloworld
maven的archetype功能可以生成各种项目的骨架。  

使用[maven-archetype-quickstart](https://maven.apache.org/archetypes/maven-archetype-quickstart/) Archetype可以生成一个最简单的maven项目：
``` bash
mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4
```
项目结构：  
```
project bash
|-- pom.xml
`-- src
    |-- main
    |   `-- java
    |       `-- $package
    |           `-- App.java
    `-- test
        `-- java
            `-- $package
                `-- AppTest.java
```

使用[maven-archetype-webapp](https://maven.apache.org/archetypes/maven-archetype-webapp/)可以生成一个jsp的web示例项目：  

``` bash
mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-webapp -DarchetypeVersion=1.4
```

项目结构：  
```
project
|-- pom.xml
`-- src
    `-- main
        `-- webapp
            |-- WEB-INF
            |   `-- web.xml
            `-- index.jsp
```

### 修改系统库
maven默认使用的系统库是1.5，如果需要修改可以在pom.xml文件properties设置中
加上这两行： 
``` xml
<project>
  [...]
  <properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>
  [...]
</project>
```

或者

``` xml
<project>
  [...]
  <build>
    [...]
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>
    </plugins>
    [...]
  </build>
  [...]
</project>
```

参考：https://maven.apache.org/plugins/maven-compiler-plugin/examples/set-compiler-source-and-target.html

设置完了如果是使用eclipse，需要在项目根目录点击右键-->maven-->update project   
如果是使用intellij idea，需要在项目根目录点击右键-->maven-->reimport  


**注意**：
如果是spring boot项目，也可以这样设置，与上面的设置等同（[参考](https://stackoverflow.com/questions/38882080/specifying-java-version-in-maven-differences-between-properties-and-compiler-p)）：  
``` xml
<properties>
     <java.version>1.8</java.version>
</properties> 
```

### 查看生效的maven设置
`mvn help:effective-settings` 可以查看生效的maven设置  

```
shiming@pro ➜  conf mvn help:effective-settings
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------< org.apache.maven:standalone-pom >-------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] --------------------------------[ pom ]---------------------------------
[INFO]
[INFO] --- maven-help-plugin:3.2.0:effective-settings (default-cli) @ standalone-pom ---
[INFO]
Effective user-specific configuration settings:

<?xml version="1.0" encoding="UTF-8"?>
<!-- ====================================================================== -->
<!--                                                                        -->
<!-- Generated by Maven Help Plugin on 2019-07-02T12:49:47+08:00            -->
<!-- See: http://maven.apache.org/plugins/maven-help-plugin/                -->
<!--                                                                        -->
<!-- ====================================================================== -->
<!-- ====================================================================== -->
<!--                                                                        -->
<!-- Effective Settings for 'shiming' on 'pro'                              -->
<!--                                                                        -->
<!-- ====================================================================== -->
<settings xmlns="http://maven.apache.org/SETTINGS/1.1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd">
  <localRepository>/Users/shiming/.m2/repository</localRepository>
  <mirrors>
    <mirror>
      <mirrorOf>central</mirrorOf>
      <name>aliyun maven</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <id>alimaven</id>
    </mirror>
    <mirror>
      <mirrorOf>central</mirrorOf>
      <name>oneof the central mirrors in china</name>
      <url>http://maven.net.cn/content/groups/public/</url>
      <id>maven.net.cn</id>
    </mirror>
    <mirror>
      <mirrorOf>central</mirrorOf>
      <name>JBoss Public Repository Group</name>
      <url>http://repository.jboss.org/nexus/content/groups/public</url>
      <id>jboss-public-repository-group</id>
    </mirror>
  </mirrors>
  <profiles>
    <profile>
      <activation>
        <activeByDefault>true</activeByDefault>
        <jdk>11</jdk>
      </activation>
      <properties>
        <maven.compiler.compilerVersion>11</maven.compiler.compilerVersion>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
      </properties>
      <id>jdk-11</id>
    </profile>
  </profiles>
  <pluginGroups>
    <pluginGroup>org.apache.maven.plugins</pluginGroup>
    <pluginGroup>org.codehaus.mojo</pluginGroup>
  </pluginGroups>
</settings>


[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.919 s
[INFO] Finished at: 2019-07-02T12:49:47+08:00
[INFO] ------------------------------------------------------------------------
```

### 修改maven设置
Mac 使用`brew`安装的`maven`，settings.xml文件路径是`/usr/local/Cellar/maven/3.6.0/libexec/conf/settings.xml`

## java常识
1. java程序编译后的.class文件是什么 https://www.geeksforgeeks.org/java-class-file/  

## troubleshoot
### 引入jpa依赖但是没有配置数据库
**问题：**  
spring boot引入jpa依赖但是没有设置数据库连接参数，运行应用报错：  
``` 
***************************
APPLICATION FAILED TO START
***************************

Description:

Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured.

Reason: Failed to determine a suitable driver class


Action:

Consider the following:
	If you want an embedded database (H2, HSQL or Derby), please put it on the classpath.
	If you have database settings to be loaded from a particular profile you may need to activate it (no profiles are currently active).
```

**解决方案：**  

1. 在application.properties文件里配置数据库连接  
```
spring.datasource.url=jdbc:mysql://localhost:3306/rule
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```
如果`com.mysql.jdbc.Driver`飘红，报can't resolve，在pom.xml中添加依赖即可：  
``` xml
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
```

也可以在yaml文件或程序中配置数据库连接  


2. 如果暂时不想配置数据库，使用以下配置设置  
1）在注解中
``` java
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
public class App {

    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }

}
```

2）在配置文件中  
```
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

参考： https://www.baeldung.com/spring-boot-failed-to-configure-data-source  

## idea技巧

## java培训
| 名称               | 语言 | 地址                                      | 备注                                     |
| ------------------ | ---- | ----------------------------------------- | ---------------------------------------- |
| guru99的文字版教程 | 英文 | https://www.guru99.com/java-tutorial.html | 整理的很好，讲到底层原理，例子不够       |
| w3school java教程  | 英文 | https://www.w3schools.com/java/           | 交互式体验，可以在线运行，还有一些小例子 |
| Java编程语言基础   | 中文 | https://www.shiyanlou.com/courses/1230    | 详略得当，在线交互式体验，入门好材料     |
|                    |      |                                           |                                          |
| Springboot quick start   | 英文 | https://www.youtube.com/watch?v=msXL2oDexqw&list=PLqq-6Pq4lTTbx8p2oCgcAQGQyqN8XeA1x    | 精心制作的springboot视频教程（youtube），每个视频很短，适合springboot入门     |
|                    |      |                                           |                                          |

## java面试
常见面试问题和解答 https://www.guru99.com/java-interview-questions-answers.html



