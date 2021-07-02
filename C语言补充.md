### 编译预处理和宏：宏定义

![image-20200729104720929](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20200729104720929.png)

```c
// 可以看到第七行代码中没有加分号
// 第12行中添加了分号
#include<cstdio>

#define PI 3.141592
#define PI2 2*PI
#define PRT printf("%f", PI); \
            printf("%f\n", PI2)
int main(){
    PRT;

    return 0;
}

```

宏可以带参数

```c
#include<cstdio>

#define cube(x) ((x)*(x)*(x))
// 也可以写成这样，但是要注意运算顺序
// #define cube(x) (x*x*x) 
int main(){
    int i = 5;
    printf("%d",cube(i));

    return 0;
}

```

要注意#define是直接替换

宏定义的结束时不要加分号

带参数的宏的原则

- 一切都要括号
- 整个值都要括号
- 参数出现的都要括号

### 大项目结构

#### 多个源代码文件

在devc++中选择新建项目

main.c

```c
#include <stdio.h>

int max(int a, int b); 
int main(int argc, char *argv[]) {
	int x = 5, y = 10;
	int temp = max(x,y);
	printf("%d", temp);
	return 0;
}
```



max.c

```c
int max(int a, int b){
	return a>b ? a : b;
}
```



- 在devc++中新建一个项目，然后把几个源代码文件加入进去
- 对于项目，devc++的编译会把一个项目中所有的源代码文件都编译后，链接起来
- 有的ide有分开的编译和构建两个按钮，前者是对单个源代码文件编译，后者是对整个项目做链接



一个.c文件是一个编译单元，编译器每次编译只编译一个编译单元

#### 头文件

- 把函数原型放到一个头文件(以.h结尾)中，在需要调用这个函数的源代码文件(.c文件)中以#include这个头文件，就能在编译器在编译的时候知道函数的原型

main.c

```c
#include <stdio.h>
#include "max.h"

//int max(int a, int b); 
int main(int argc, char *argv[]) {
	int x = 5, y = 10;
	int temp = max(x,y);
	printf("%d", max(x,y));
	
	return 0;
}
```



max.c

```c
#include "max.h"

int max(int a, int b){
	return a>b ? a : b;
}
```



max.h

```c
int max(int a, int b);
```



**#include**

- #include是一个编译预处理指令，和宏一样，在编译之前就处理了
- 它把那个文件的全部文本内容原封不动地插入到它所在的地方
- 所以也不是一定要在.c文件的最前面#include

**""还是<>**

- #include有两种形式来指出要插入的文件
- ""要求编译器首先在当前目录(.c文件所在的目录)寻找这个文件，如果没有，到编译器指定的目录去找
- <>让编译器只在指定的目录去找
- 编译器自己知道自己的标准库的头文件在哪里
- 环境变量和编译器命令行参数也可以指定寻找头文件

**#include的误区**

- #include不是用来引入库的
- stdio.h里面只有printf的原型，printf的代码在另外的地方，某个.lib(Windows)或者.a(Unix)中
- 现在的C语言编译器默认会引入所有的标准库
- #include<stdio.h>只是为了让编译器知道printf函数的原型，保证在调用时给出的参数值是正确的类型

**头文件**

- 在使用和定义这个函数的地方都应该#include这个头文件
- 一般的做法就是任何.c都有对应的同名.h，吧所有对外开放的函数的原型和全局变量的声明都放进去

**不对外公开的函数**

- 在函数前面加上static就使得它成为只能在所在的编译单元中被使用的函数
- 在全局变量前面加上static就使得它成为只能在所在的编译单元中被使用的全局变量

#### 声明

main.c

```c
#include <stdio.h>
#include "max.h"

//int max(int a, int b); 
int main(int argc, char *argv[]) {
	int x = 5, y = 10;
	int temp = max(x,y);
	printf("%d", max(x,gAll));
	
	return 0;
}
```

max.c

```c
#include "max.h"
int gAll = 6;
int max(int a, int b){
	return a>b ? a : b;
}
```

max.h

```c
int max(int a, int b);
extern int gAll; 
```

**变量的声明**

- int i;是变量的定义
- extern int i;是变量的声明

**声明和定义**

- 声明式不产生代码的东西，如函数原型，变量声明，结构声明，宏声明，枚举声明，类型声明，inline函数
- 定义是产生代码的东西

**头文件**

- 只有声明可以被放在头文件中
- 是规则不是法律
- 否则会造成一个项目中多个编译单元中有重名实体
- **某些编译器允许几个编译单元中存在同名的函数，或者用weak修饰符来强调这种存在**

**重复声明**

- 同一个编译单元里，同名的结构不能被重复声明
- 如果你的头文件里有结构的声明，很难这个头文件不会在一个编译单元里被#include多次
- 所以需要“标准头文件结构”

先看一下错误演示

main.c

```c
#include <stdio.h>
#include "max.h"
#include "min.h"

//int max(int a, int b); 
int main(int argc, char *argv[]) {
	int x = 5, y = 10;
	int temp = max(x,y);
	printf("%d", max(x,gAll));
	
	return 0;
}
```



max.c

```c
#include "max.h"

int gAll = 6;
int max(int a, int b){
	return a>b ? a : b;
}
```



max.h

```c
int max(int a, int b);
extern int gAll; 

struct Node{
	char* name;
	int age;
};
```



min.h

```c
#include "max.h"
```



报错如下，提示重复定义了struct Node

![image-20200729151741288](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20200729151741288.png)

需要将max.h修改成如下样子，这里的#if是预处理器-条件编译的知识

```c
// 保证这个头文件在一个编译单元中只会被#include一次
// vs中pragma once也能起到相同的作用，但不是左右的编译器都支持
#ifndef _MAX_H_
#define _MAX_H_

int max(int a, int b);
extern int gAll; 

struct Node{
	char* name;
	int age;
};

#endif
```



### 链表

```c
#include<stdio.h>
#include<stdlib.h>

typedef struct _node{
	int value;
	struct _node *next;
} Node;

typedef struct _list{
	Node* head;
	Node* tail;
} List;

void add(List* plist, int num);
void print(List* plist);

int main(){
	List list;
	list.head = list.tail = NULL;
	int num;
	do{
		scanf("%d", &num);
		if(num != -1){
			add(&list, num);
		}
	} while (num != -1);
	
	print(&list);
	
	scanf("%d", &num);
	Node *p;
	int isFound = 0;
	for(p=list.head; p; p=p->next){
		if(p->value == num){
			printf("找到\n");
			isFound = 1;
			break;
		}
	}
	if(!isFound) printf("未找到\n"); 
	
	Node *q;
	scanf("%d", &num);
	for(q=NULL,p=list.head; p; q=p,p=p->next){
		if(p->value == num){
			if(q){
				q->next = p->next;
			}else{
				list.head = p->next;
			}
			free(p);
			break;
		}
	}
	
	print(&list);
	
	for(p=list.head; p; p=q){
		q = p->next;
		free(p);
	} 
	
	
	return 0;
} 

void add(List* plist, int num){
	// 添加 
	Node *p = (Node *) malloc (sizeof(Node));
	p->value = num;
	p->next = NULL;
	// 找到最后一个
	Node * last = plist->head; 
	if(last){
		while(last->next){
			last = last->next;
		}
		// 添加上去
		last->next = p;
		plist->tail = p;
	}else{
		plist->head = p;
		plist->tail = p;
	}
}

void print(List* plist){
	Node *p;
	for(p = plist->head; p; p=p->next){
		printf("%d\t",p->value);
	}
	printf("\n");
}
```



















