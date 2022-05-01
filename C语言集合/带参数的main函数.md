```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h> 
void processUserInputStr(char* s);
int main(int argc,char* argv[])
{
    processUserInputStr(argv[1]);
    return 0;
}
void  processUserInputStr(char* s)
{
	double a,b;
    char op;
	int i=0;
	
    char strA[100],strB[100];
    while(s[i]!='+' && s[i]!= '*'){
    	strA[i]=s[i];
    	i++;
	}
	strA[i]='\0'; 
	a=atof(strA);
	op=s[i];
	i++;
	int j=0;
	while(s[i]!='\0'){
		strB[j]=s[i];
		i++;
		j++;
	}
	strB[j]='\0';
	b=atof(strB);
	if(op=='+') printf("%.2f",a+b);
    else printf("%.2f",a*b);
}
```

![image-20211219215347792](C:\Users\17675\AppData\Roaming\Typora\typora-user-images\image-20211219215347792.png)

第一步：指定路径；

第二步：写参数，注意第一个是文件名.exe格式