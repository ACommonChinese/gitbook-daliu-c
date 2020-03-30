# struct

### 结构体类型  

```C
struct tag { 
    member-list
    member-list 
    member-list  
    ...
} variable-list ;
```

**tag** 是结构体标签。
**member-list** 是标准的变量定义，比如 int i; 或者 float f，或者其他有效的变量定义。
**variable-list** 结构变量，定义在结构的末尾，最后一个分号之前，您可以指定一个或多个结构变量

在一般情况下，**tag、member-list、variable-list** 这 3 部分至少要出现 2 个。以下为实例：

```C
struct {
    int a;
    char b;
    double c;
} s1;

s1.a = 10;
printf("%d\n", s1.a);

struct SIMPLE {
    int a;
    char b;
    double c;
};
struct SIMPLE s2;
s2.a = 10;
printf("%d\n", s2.a);
struct SIMPLE s2, s3;
s3.a = 10;
printf(s3.a);
```

### typedef struct 

```c
// 也可以用typedef创建新类型
typedef struct
{
    int a;
    char b;
    double c;
} Simple2;

int main(int argc, const char * argv[]) {
    // 现在可以用Simple2作为类型声明新的结构体变量
    Simple2 u1, u2[20], *u3;
    u1.a = 10;
    u1.b = 'c';
    u1.c = 'h';
    u2[0] = u1;
    Simple2 first = u2[0];
    printf("%d\n", first.a); // 10
    
    u3 = &u1;
    printf("%c\n", u3->b); // c
    
    return 0;
}
```

### 结构体变量的初始化  

```c
struct Book {
    char title[50];
    char author[20];
    char subject[100];
    int book_id;
} book = {"C 语言", "ROB", "编程语言", 123456};

int main(int argc, const char * argv[]) {
    printf("title : %s\nauthor: %s\nsubject: %s\nbook_id: %d\n", book.title, book.author, book.subject, book.book_id);
    return 0;
}
```

### 结构体作为函数参数   
```c
#include <stdio.h>
#include <string.h>

struct Book {
    char title[50];
    char author[50];
    char subject[100];
    int book_id;
};

void printBookInfo(struct Book book) {
    printf("=============================\n");
    printf("title: %s\n", book.title);
    printf("author: %s\n", book.author);
    printf("subject: %s\n", book.subject);
    printf("book_id: %d\n", book.book_id);
    printf("=============================\n");
}

int main(int argc, const char * argv[]) {
    struct Book book1;
    strcpy(book1.title, "C Programming");
    strcpy(book1.author, "Nuha Ali");
    strcpy(book1.subject, "C Programming Tutorial");
    book1.book_id = 6495407;
    printBookInfo(book1);
    return 0;
}
```

### 指向结构体的指针  

```c
void printBookInfo(struct Book *book) {
    printf("=============================\n");
    printf("title: %s\n", book->title);
    printf("author: %s\n", book->author);
    printf("subject: %s\n", book->subject);
    printf("book_id: %d\n", book->book_id);
    printf("=============================\n");
}
```

### 内存对齐

先看一个示例：  

```C
struct A {
    int a;
    char b;
    char c;
} a;

struct B {
    char a;
    int b;
    char c;
} b;

int main(int argc, const char * argv[]) {
    printf("%lu\n", sizeof(a)); // 8
    printf("%lu\n", sizeof(b)); // 12
    return 0;
}
```

对于相同元素但排序不同而导致的占用内存不同，这就是由于内存对齐导致的，那么为什么需要内存对齐呢？原因是：
1. 平台原因(移植原因)：不是所有的硬件平台都能访问任意地址上的任意数据的；某些硬件平台只能在某些地址处取某些特定类型的数据，否则抛出硬件异常
2. 性能原因：数据结构(尤其是栈)应该尽可能地在自然边界上对齐。原因在于，为了访问未对齐的内存，处理器需要作两次内存访问；而对齐的内存访问仅需要一次访问. 也就是说为了节省时间。这和C本身的设计相关。

**C语言结构体内存对齐的原则 (假设无#pragma pack宏)**  

首先需要了解自射对齐值，自射对齐值=min(类型大小，默认对齐参数)，比如系统

1. struct或union中的数据成员，第一个数据成员放在offset为0的地方，

### 位域  


