step1: open a file

step2: R/W from/to the file

step3: close the file 

```c
void main(void)
{
	FILE *p;
	if((p=fopen("文件名","r或w"))==NULL){
		puts("file open failure");
		return;
		}
	char c;
	while(1){
		//c=fgetc(p),读取内容
		if((c=fgetc(p))==EOF) break;
		fputc(c,stdout);
	}
	fclose(p);
}
```



主函数

```c
void main(int count,char* name[])
{
	if(count==1) printf("count=1");
	puts(name[0]);
	
    else(count==2) printf("count=2");
    puts(name[0]);puts(name[1]);

    else(count==3) printf("count=3");
    puts(name[0]);puts(name[1]);puts(name[2]);
    
    else printf("count is too luosuo");
    
 
}
```

主函数要在命令提示框中进行调用

c=fgetc(fp)；读取字符

fputc(c,stdout);打印字符到窗口

fputs(c,fp);打印字符到文件fp

fclose(fp);关闭文件

feof(fp);表示文件结束返回1，与循环连用，可用于文件读取是否完成

判断字符读取是否结束也可以用(c!=EOF)

stu[6];

fwrite(stu,sizeof(struct),6,fp);stu[]表示一个结构体数组，6表示它的个数，它可以把所有数据读入到文件中

fread(stu,sizeof(struct,6,fp));从文件中读入到结构体数组中

数据块的保存和加载：

```c
void SaveResult(const char *fileName, STUDENT stud[],int n,int m)
{
  FILE *fp = fopen(fileName,"w");
  if(fp == NULL)
  {
    printf("Failure to open %s!\n",fileName);
    exit(0);
  }
  fwrite(&n,sizeof(n),1,fp);
  fwrite(&m,sizeof(m),1,fp);
  fwrite(stud,sizeof(STUDENT),n,fp);
  fclose(fp);
}


```

```c
void ReadStudInfo(const char *fileName, STUDENT stud[])
{
    FILE *fp = fopen(fileName,"r"); 
    if(fp == NULL)
    {
        printf("Failure to open %s!\n",fileName);
        exit(0);
    }
    int n,m;
    fread(&n,sizeof(n),1,fp);
    fread(&m,sizeof(m),1,fp);
    fread(stud,sizeof(STUDENT),n,fp);
    fclose(fp);
}
```

格式化的保存和加载:

```c
void SaveResult(const char *fileName, STUDENT stud[],int n,int m)
{
	FILE *fp = fopen(fileName,"w");  
	if(fp == NULL)
    {
        printf("Failure to open %s!\n",fileName);
        exit(0);
    }
    fprintf(fp,"%d %d",n,m);
    for(int i=0;i<n;i++)
	{
        fprintf(fp,"\n%-12ld\t",stud[i].studentID);
        fprintf(fp,"%-12s\t",stud[i].studentName);
        fprintf(fp,"%-4s\t",stud[i].sex);
        fprintf(fp,"%4d-%02d-%02d\t",stud[i].birthday.year,stud[i].birthday.month,stud[i].birthday.day);
        for(int j=0;j<m;j++)
            fprintf(fp,"%.0f\t",stud[i].score[j]);
        fprintf(fp,"%.0f\t",stud[i].total);
		fprintf(fp,"%.0f\t",stud[i].average);
		fprintf(fp,"%d\t",stud[i].rank);
	}
	fclose(fp);
}
```

```c
void ReadStudInfo(const char *fileName, STUDENT stud[])
{
	FILE *fp = fopen(fileName,"r"); 
    if(fp == NULL)
    {
        printf("Failure to open %s!\n",fileName);
        exit(0);
    }
    int n,m;
    fscanf(fp,"%d%d",&n,&m);
    for(int i=0;i<n;i++)
    {
        fscanf(fp,"%ld",&stud[i].studentID);
        fscanf(fp,"%s",stud[i].studentName);
        fscanf(fp,"%s",stud[i].sex);
        fscanf(fp,"%d-%d-%d",&stud[i].birthday.year,&stud[i].birthday.month,&stud[i].birthday.day);
        for(int j=0;j<m;j++)
        	fscanf(fp,"%f",&stud[i].score[j]);
    }
    fclose(fp);
}
```

