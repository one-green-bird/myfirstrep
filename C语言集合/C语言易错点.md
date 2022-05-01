1、double类型变量的格式化输入是scanf(“%lf",&a)；

2、for循环如果不加{}只会执行后面的第一条语句；

3、数组指针和指针数组

[(9条消息) 数组指针和指针数组_mick_hu的博客-CSDN博客_数组指针](https://blog.csdn.net/mick_hu/article/details/100931034?ops_request_misc=%7B%22request%5Fid%22%3A%22164066504316780271939745%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=164066504316780271939745&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-100931034.pc_search_es_clickV2&utm_term=数组指针和指针数组&spm=1018.2226.3001.4187)

数组的指针：是一个指针，什么样的指针呢？指向数组的指针。

指针的数组：是一个数组，什么样的数组呢？装着指针的数组。

然后，需要明确一个优先级顺序：()>[]>*，所以：

(*p)[n]：根据优先级，先看括号内，则p是一个指针，这个指针指向一个一维数组，数组长度为n，这是“数组的指针”，即数组指针；

\*p[n]：根据优先级，先看[]，则p是一个数组，再结合*，这个数组的元素是指针类型，共n个元素，这是“指针的数组”，即指针数组。

```c
int *p1[5]；
int (*p2)[5]；
```

数组指针 (*p)[n]

数组指针：是指针——指向数组的指针。

对数组指针取*得到该指针指向的数组的首地址；

例p[0]==\*p,都是第一个数组的首地址；p[1]==\*(p+1),下一个数组的首地址；

通过数组指针对二维数组的遍历：

```c
    int a[2][3]={{1,2,3},{4,5,6}}
    int i,j;
    int (*p)[3]=a;

    for(i=0;i<2；i++)
        for(j=0;j<3;j++)
            printf("%d ",*( *(p+i)+j ) );

```

可以清楚的看到其实p[0],p[1]表示的都是首地址；

4、动态二维数组的的开辟：

```c
    char **str;
    int n,i;
    scanf("%d",&n);

    str=(char**)malloc(n*sizeof(char*));
    for(i=0;i<n;i++) *(str+i)=(char*)malloc(20*sizeof(char));

```

5、对于字符串的输入，gets() 和 scanf()的选择；

1）如果输入的字符串没有空白字符，优先选择scanf()，因为它不用考虑缓冲区的问题；

2）否则选择gets()，gets()每一次会从输入流读取一整行，但是gets()需要注意缓冲区的问题；

如下图代码所示，如果敲入数字a后，键入换行，就不会再等待输入字符串了，因为gets()会读入换行；

```c
	int a;
	char str[20];
	scanf("%d",&a);
	gets(str);
	printf("%s",str);
```

6、全局变量和局部变量的区别：(Ctrl+点击)可实现跳转

[(9条消息) C语言全局变量和局部变量总结_谦190的博客-CSDN博客_c语言全局变量](https://blog.csdn.net/u013355826/article/details/53224303?ops_request_misc=&request_id=&biz_id=102&utm_term=局部变量&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-53224303.pc_search_es_clickV2&spm=1018.2226.3001.4187)

<img src="C:\Users\17675\AppData\Roaming\Typora\typora-user-images\image-20211228175826917.png" alt="image-20211228175826917" style="zoom: 25%;" />

6、枚举类型：

枚举类型同结构体类型相似；

```c
#include<stdio.h>
enum Weeday{Sunday,Monday,Tuesday=5,Wednesday,Thursday,Friday,Saturday};
int main()
{
	enum Weeday today;
	today=Saturday;
	printf("today=%d",today);
	return 0;
 } 
```

如上面代码所示，如果对Tuesday=5,则其后面的会相应的递增,Wednesday=6;但是前面的不受影响，Sunday=0,Monday=1;

7、写编程题时先把三个头文件写上；
