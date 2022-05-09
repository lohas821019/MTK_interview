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

for (i = 0, j = 1; i < 5; i++) // 3, 5, 9, 17, 33

    INC(j); // 1, 2, 4, 8, 16

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



# 23 下面尚未補齊
https://hackmd.io/@Rance/SkSJL_5gX?type=view

http://arc2453.blog.fc2.com/blog-entry-31.html
