# 0 線上Compiler

https://www.onlinegdb.com/

<br/>

# 1
https://www.raind.blog/c&cpp-zh/c&cpp_interviewexam.html
```
#define MUX(a, b) a*b

MUX(10+5, 10-5) = ?
```
<br/>

# 2

```
unsigned long v1 = 0x00001111;
unsigned long v2 = 0x00001202;
unsigned long v;

v = v1&(~v2);
v = v | v2;

//求 v = ?
```
<br/>

# 3

用一行程式碼判斷是否為2的冪次方?

<br/>

# 4

https://www.796t.com/content/1545714542.html
```
int a[5] = {1, 2, 3, 4, 5};
int *p = (int*)(&a+1);

// Ask: the value of *(a+1) and *(p-1)?
```
<br/>

# 5

```
Int a[] = {6, 7, 8, 9, 10};
Int *p=a;

*(p++)+=123;
*(++p)+=123;

// Ask: the content of array a?
```
<br/>

# 6

```
int fun(int x)
{
    Int count = 0;

    while(x){

    count++;
	printf("%i",count);

    x = x & (x-1)
}

return count;

}

fun(456) + fun(123) + fun(789) = ?
```

<br/>

# 7 觀念:for沒括號的話，只有最接近那行會進入迴圈。

```
#define INC(x) x*=2; x+=1

int main()
{

int i, j;

for (i = 0, j = 1; i < 5; i++)

    INC(j);

    printf("j = %d\n", j);

}

//求J輸出值是多少?
```
<br/>

# 8

```
int a = 25;

int b = 30;

int ques1 = a++ + b++;

int ques2 = ++a + ++b;

printf("%d, %d", ques1, ques2)
```

<br/>

# 9

https://jaime-lin.medium.com/%E8%81%AF%E7%99%BC%E7%A7%91-c%E8%AA%9E%E8%A8%80%E6%B8%AC%E8%A9%A6%E9%A1%8C%E7%9B%AE-7097f09add02
```
#include <stdio.h>

int c;

int func(int m, int* n){
    c += 1;
    m += c;
    *n += m;
    return m;
}

int main(void) {
	c = 0;
	int x = 5;
	int y = 7;
	int z;
	x = func(x, &y);
	z = func(x, &y);
	printf("sum of x, y, z, and c = %d", x + y + z + c);
	return 0;
}

//求印出來的數值
```
<br/>

# 10


```
#include <stdio.h>

int c;

int func(int n){
    c *= n;
    return n;
}

int main(void) {
	c = 1;
	int n = 2;
	func(func(func(func(func(func(func(func(n))))))));
	printf("c = %d", c);
	return 0;
}

//求印出來的數值
```

<br/>

# 11

```
#include <stdio.h>
#define ADD(a,b) a+b

int main(void) {
	int m = 5, n = 10;
	int p = ADD(m, n) * 5;
	printf("p = %d", p);
	return 0;
}

//求印出來的數值
```

<br/>

# 12

#include <stdio.h>

```
int main(void) {
	char *str[] = {
	    {"MediaTekOnlineTesting"},
	    {"WelcomeToHere"},
	    {"Hello"},
	    {"EverydayGenius"},
	    {"HopeEverythingGood"}
	};

	char* m = str[4] + 4;
	char* n = str[1];
	char* p = *(str+2) + 4;
	printf("1. %s\n", *(str+1));
	printf("2. %s\n", (str[3]+8));
	printf("3. %c\n", *m);
	printf("4. %c\n", *(n+3));
	printf("5. %c\n", *p + 1);
	return 0;
}
```

<br/>

# 13

1. 一個整型數（An integer）
2. 一個指向整型數的指標（A pointer to an integer）
3. 一個指向指標的的指標，它指向的指標是指向一個整型數（A pointer to a pointer to an integer）
4. 一個有10個整型數的陣列（An array of 10 integers）
5. 一個有10個指標的陣列，該指標是指向一個整型數的（An array of 10 pointers to integers）
6. 一個指向有10個整型數陣列的指標（A pointer to an array of 10 integers）
7. 一個指向函數的指標，該函數有一個整型參數並返回一個整型數（A pointer to a function that takes an integer as an argument and returns an integer）
8. 一個有10個指標的陣列，該指標指向一個函數，該函數有一個整型參數並返回一個整型數（ An array of ten pointers to functions that take an integer argument and return an integer）

// 寫出上述所述之指標


<br/>

# 14 Swap 的各種寫法 (bitwise ,指標)
http://puremonkey2010.blogspot.com/2011/05/c-bitwise-operation.html


<br/>

# 15

https://leetcode.com/problems/maximum-subarray/


<br/>

# 16

https://mkfsn.blogspot.com/2016/12/blog-post.html


Explain "#error"


<br/>

# 17

Explain "struct" and "union"?


<br/>

# 18

Explain "volatile". Can we use "const" and "volatile" in the same variable? Can we use "volatile" in a pointer?

<br/>

# 19

write a code

a. set the specific bit

b. clear the specific bit

c. inverse the specific bit (0->1; 1->0)


<br/>

# 20
Fill the blank
```
void(*(*papf)[3])(char *); // Rewrite this
typedef ___________;
pf(*papf)[3];
```

<br/>

# 21

Write a code that check the input is a multiple of 3 or not without using division or mod


<br/>

# 22

Explain lvalue and rvalue.


<br/>

# 23
https://hackmd.io/@Rance/SkSJL_5gX?type=view

```
extern void func1(void);
extern void func2(void);
extern void func3(void);
extern void func4(void);
extern void func5(void);

void main(int n)
{
  if n==1 execute func1;
  if n==2 execute func2;
  if n==3 execute func3;
  if n==4 execute func4;
  if n==5 execute func5;
}

```

<br/>

# 24

```
extern void func1(void);
extern void func2(void);
extern void func3(void);
extern void func4(void);
extern void func5(void);

void main(int n)
{
  if n==33 execute func1;
  if n==67 execute func2;
  if n==324 execute func3;
  if n==231 execute func4;
  if n==687 execute func5;
}

```

<br/>

# 25
寫一個 function 可傳入正整數參數 N，回傳 1 + 2 + 3 +…+N 的和


<br/>

# 26  寫出3種反轉字元的方式

reverse a string


<br/>

# 27

寫一個“標準”巨集MIN ，這個巨集輸入兩個參數並返回較小的一個。


<br/>

# 28
Write a MARCO to calculate the square of integer a.

<br/>

# 29
Write a function to find the middle field of singled-linked list without traverse whole list.

<br/>

# 30
Write a code to reverse the linked list.

For example: [0] -> [n], [1]->[n-1],…[n]->[0].

<br/>

# 31
Find the possible error
```
Int ival;
Int **p;
Ival = *p;
```

<br/>

# 32
What is the possible error of below SQR function.

```
int SQR(volatile int *a){
   return (*a)*(*a);
}
```

<br/>

# 33
用預處理指令#define 聲明一個常數，用以表明1年中有多少秒（忽略閏年問題）

<br/>

# 34
http://arc2453.blog.fc2.com/blog-entry-31.html


Global 直接宣告參數不給值
跟function 裡面宣告參數不給值
直接印會印出什麼?


兩個 String還是Char陣列
分別丟同樣的字串
問如果直接 == 會有什麼樣的結果
true,false或不能編譯

<br/>

```
SWAP( int*a, int*b){
temp=a;
b=a;
b=temp;}
```
extern / inline / intern

C裡面的memory
程式段(.text)主要存放程式的機器碼，
資料段(.data)則是存放全域變數的資料，
BSS 段(.bss)存放的是未初始化的全域變數，
堆積段(.heap)程式使用 malloc 進行記憶體分配時，可以分配的動態記憶空間
堆疊段(.stack)則存放「參數、函數返回點、區域變數、框架指標」等資料
有出多選題問Stack裡面放什麼資料




