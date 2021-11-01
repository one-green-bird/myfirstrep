sprintf函数的用法
1、该函数包含在stdio.h的头文件中。
2、sprintf和平时我们常用的printf函数的功能很相似。sprintf函数打印到字符串中（要注意字符串的长度要足够容纳打印的内容，否则会出现内存溢出），而printf函数打印输出到屏幕上。sprintf函数在我们完成其他数据类型转换成字符串类型的操作中应用广泛。
3、sprintf函数的格式：
int sprintf( char *buffer, const char *format [, argument,…] );
除了前两个参数固定外，可选参数可以是任意个。buffer是字符数组名；format是格式化字符串（像：”%3d%6.2f%#x%o”,%与#合用时，自动在十六进制数前面加上0x）。只要在printf中可以使用的格式化字符串，在sprintf都可以使用。其中的格式化字符串是此函数的精华。
printf 和sprintf都使用格式化字符串来指定串的格式，在格式串内部使用一些以”%”开头的格式说明符来占据一个位置，在后边的变参列表中提供相应的变量，最终函数就会用相应位置的变量来替代那个说明符，产生一个调用者想要的字符串。
4、可以控制精度
char str[20];
double f=14.309948;
sprintf(str,”%6.2f”,f);
5、可以将多个数值数据连接起来
char str[20];
int a=20984,b=48090;
sprintf(str,”%3d%6d”,a,b);
str[]=”20984 48090”
6、可以将多个字符串连接成字符串
char str[20];
char s1[5]={‘A’,’B’,’C’};
char s2[5]={‘T’,’Y’,’x’};
sprintf(str,”%.3s%.3s”,s1,s2);
%m.n在字符串的输出中，m表示宽度，字符串共占的列数；n表示实际的字符数。%m.n在浮点数中，m也表示宽度；n表示小数的位数。
7、可以动态指定，需要截取的字符数
char str[20];
char s1[5]={‘A’,’B’,’C’};
char s2[5]={‘T’,’Y’,’x’};
sprintf(str,”%.*s%.*s”,2,s1,3,s2);
sprintf(str, “%*.*f”, 10, 2, 3.1415926);
8、可以打印出i的地址
char str[20];
int i;
sprintf(str, “%p”, &i);
上面的语句相当于
sprintf(str, “%0*x”, 2 * sizeof(void *), &i);
9、sprintf的返回值是字符数组中字符的个数，即字符串的长度，不用在调用strlen(str)求字符串的长度。
10、使用字符指针指向的字符串来接收打印的内容
例子：

int main()
{
    int ddd=666;
    char *buffer=NULL;    
    if((buffer = (char *)malloc(80*sizeof(char)))==NULL)
    {
        printf("malloc error\n");
    }
    sprintf(buffer, "The value of ddd = %d", ddd);//The value of ddd = 666
    printf("%s\n",buffer);
    free(buffer);
    buffer=NULL;
    return 0;
}
1
2
3
4
5
6
7
8
9
10
11
12
13
14
指针刚开始定义的时候，并不指向所处，可以指向一个变量，然后可以用，如果要单纯用这个指针，那么要给这个指针malloc分配一片内存，加了malloc就要加stdlib.h
11、设想当你从数据库中取出一条记录，然后希望把他们的各个字段按照某种规则连接成一个字符串时，就可以使用这种方法，从理论上讲，他应该比strcat 效率高，因为strcat 每次调用都需要先找到最后的那个字符串结束字符’\0的位置，而在上面给出的例子中，我们每次都利用sprintf 返回值把这个位置直接记下来了。
例子：

void main(void)
{ 
    char buffer[200], s[] = "computer", c = 'l'; 
    int i = 35, j; 
    float fp = 1.7320534f; // 
    j = sprintf( buffer, " String: %s\n", s ); // 
    j += sprintf( buffer + j, " Character: %c\n", c ); // 
    j += sprintf( buffer + j, " Integer: %d\n", i ); // 
    j += sprintf( buffer + j, " Real: %f\n", fp );// 
    printf( "Output:\n%s\ncharacter count = %d\n", buffer, j );
}
1
2
3
4
5
6
7
8
9
10
11
该例子是将所有定义的数据和格式控制块中的字符连接在一起，最后打印出来buffer的内容和字符串中字符的个数。
结果如图所示：


12、 格式化数字字符串
sprintf最常见的应用之一莫过于把整数打印到字符串中。如：
（1）把整数123打印成一个字符串保存在s中。
sprintf(s, “%d”, 123); //产生“123″
（2）可以指定宽度，不足的左边补空格：
sprintf(s, “%8d%8d”, 123, 4567); //产生：“ 123 4567″
当然也可以左对齐：
sprintf(s, “%-8d%8d”, 123, 4567); //产生：“123 4567″
（3）也可以按照16进制打印：
sprintf(s, “%8x”, 4567); //小写16进制，宽度占8个位置，右对齐
sprintf(s, “%-8X”, 4568); //大写16进制，宽度占8个位置，左对齐
这样，一个整数的16进制字符串就很容易得到，但我们在打印16进制内容时，通常想要一种左边补0的等宽格式，那该怎么做呢？很简单，在表示宽度的数字前面加个0就可以了。
sprintf(s, “%08X”, 4567); //产生：“000011D7″
上面以”%d”进行的10进制打印同样也可以使用这种左边补0的方式。
这里要注意一个符号扩展的问题：比如，假如我们想打印短整数
（4）（short）-1的内存16进制表示形式，在Win32平台上，一个 short型占2个字节，所以我们自然希望用4个16进制数字来打印它：
short si = -1;
sprintf(s, “%04X”, si);
产生“FFFFFFFF，怎么回事？因为 sprintf是个变参函数，除了前面两个参数之外，后面的参数都不是类型安全的，函数更没有办法仅仅通过一个“%X”就能得知当初函数调用前参数压栈时 被压进来的到底是个4字节的整数还是个2字节的短整数，所以采取了统一4字节的处理方式，导致参数压栈时做了符号扩展，扩展成了32位的整数-1，打印时 4个位置不够了，就把32位整数-1的8位16进制都打印出来了。如果你想看si的本来面目，那么就应该让编译器做0扩展而不是符号扩展（扩展时二进制左边补0而不是补符号位）：
sprintf(s, “%04X”, (unsigned short)si);
就可以了。或者：
unsigned short si = -1;
sprintf(s, “%04X”, si);
sprintf和printf还可以按8进制打印整数字符串，使用”%o”。注意8进制和16进制都不会打印出负数，都是无符号的，实际上也就是变量的内部编码的直接用16进制或8进制表示。

