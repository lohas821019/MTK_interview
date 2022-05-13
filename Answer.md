# 0 線上Compiler

https://www.onlinegdb.com/


## 標註覺得困難的題型 (多複習)

21 23 24 26 29 30 44 45 

概念複習要多看:12 13 14 34 36 37 38 39


<br/>
<br/>

2022/05/12 04:15 pm 更新
<br/>

# 1
https://www.raind.blog/c&cpp-zh/c&cpp_interviewexam.html
```
#define MUX(a, b) a*b

MUX(10+5, 10-5) = ?
```

MUX取代下方式子，10+5*10-5 =10+50-5 =55

<br/>
Ans: 55 

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
v1 = 0001 0001 0001 0001 

v2 = 0001 0010 0000 0010

~v2 = 1110 1101 1111 1101

<br/>

0001 0001 0001 0001 

1110 1101 1111 1101 &

/---------------------------/

0000 0001 0001 0001

<br/>
v = v1&(~v2) = 0000 0001 0001 0001

<br/>

0001 0001 0001 0001 

0001 0010 0000 0010 |

/---------------------------/

0001 0011 0001 0011

<br/>

v = v | v2 = 0001 0011 0001 0011 = 0x00001313


<br/>
Ans: v = 0x00001313

<br/>

# 3

用一行程式碼判斷是否為2的冪次方?

Ans:

```
bool isPowerBy2(int n)
{
    return n > 0 && (n & n - 1) == 0;
}
```

<br/>

# 4

https://www.796t.com/content/1545714542.html
```
int a[5] = {1, 2, 3, 4, 5};
int *p = (int*)(&a+1);

// Ask: the value of *(a+1) and *(p-1)?
```

&a => a[0]的位置

int *p = (int*)(&a+1); => 代表是記憶體中 &a位置 +sizeof(a) = 4*5 =20byte ， &a位置往後20byte (int = 4 byte)

因此 *p 指向的位置可以當作是下一個要放a[5]的地方，也是下一個a[5]的a[0]位置 ，可以看成 a[5]

因此 *(p-1) = a[5-1] = a[4] = 5


<br/>
Ans:

*(a+1) = a[0+1] = a[1] = 2

*(p-1) = a[5-1] = a[4] = 5

<br/>
# 5

```
Int a[] = {6, 7, 8, 9, 10};
Int *p=a;

*(p++)+=123;
*(++p)+=123;

// Ask: the content of array a?
```

Int* p = a , p指向 a[0]位置, *p = 6

*(p++)+=123 (後加是計算完再加)

順序為 *p = *p +123,輸出結果後最後 *(p+1)。

*(++p)+=123;

順序為 *(p+1) ,輸出結果後最後 *p = *p +123。

<br/>

Ans: a ={129,7,131,9,10}

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

代值進入運算，EX:7 

0111    //count +1

0110 &

/---------/

0110    //count +1

0101 &

/---------/

0100    //count +1

0011 &   
/---------/

0000

0111 => 共有3個1 因此，此式子可以判斷轉乘2進制有幾個1

456 = 0100 0101 0110  => 5

123 = 0001 0010 0011  => 4

789 = 0111 1000 1001  => 6

<br/>
Ans:
fun(456) + fun(123) + fun(789) =5+4+6 =15


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

x = (x*=2)^5 +1

1*2 = 2
2*2 = 4
4*2 = 8
8*2 = 16
16*2 =32

32+1 =33

<br/>
Ans = 33

<br/>

# 8

```
int a = 25;

int b = 30;

int ques1 = a++ + b++;

int ques2 = ++a + ++b;

printf("%d, %d", ques1, ques2)
```

ques1 = a++ + b++ ;

ques1 = 25+30 = 55;

ques2 = ++a + ++b;

ques2 = (1+26) + (1+31) = 59

<br/>
Ans =59 

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

x = func(x, &y); //5 ,&7

=>  
c = 1; 

m = 5+1 = 6;

*n = *n + m =7+6 = 13

x = 6

z = func(x, &y); //6 ,&7

c = 2;

m = 6 + 2 = 8;

*n = *n + m  = 13 + 8 = 21 (y的地址)

z = 8

printf("sum of x, y, z, and c = %d", x + y + z + c);

x+y+z+c = 6 + 21 + 8 + 2 = 37

Ans: 37

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

c = c*n;

1*2 = 2 ;

2*2 = 4 ;

發現總共有8個func，因此2^8 = 4*4*4*4 = 256
<br/>

Ans: 256

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
ADD(m,n) = 5+10*5 = 55

<br/>
Ans: 55

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
---

*str = str[0]

*(str+1) = str[1] = "WelcomeToHere"

---

str[3] = EverydayGenius

(str[3]+8) = Genius

---

str[4] = HopeEverythingGood
char* m = str[4] + 4 = E (因為是字元指針+4)

---

str[1] = "WelcomeToHere"
char* n = str[1]; //指向'W'
*(n+3) = c

---

char* p = *(str+2) + 4;

*str = str[0]

*(str+2) = str[2];

str[2] = Hello;

str[2] + 4 = 'o'

*p + 1 => p + 1byte = p // o 下一個字母是 p


<br/>
Ans: 

1. WelcomeToHere
2. Genius
3. E
4. c
5. p


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

[bitwise解法](http://puremonkey2010.blogspot.com/2011/05/c-bitwise-operation.html)

```
int main(void) {
    
    int a = 10;
    int b = 20;
    
    printf("%d\n",a);
    printf("%d\n",b);
    
    a = a^b;
    b = a^b;
    a = a^b;
    
    printf("%d\n",a);
    printf("%d\n",b);
}
```

[指標解法](https://www.796t.com/content/1549322654.html)

```
#include <stdio.h>

void swap(int* a, int* b){
    int temp;
    temp = *a;
    *a = *b ;
    *b = temp;
}

int main(void) {
    
    int a = 10;
    int b = 20;
    
    int * pa = &a;
    int * pb = &b;
    
    printf("%p\n",pa);
    printf("%p\n",pb);
    
    printf("%d\n",a);
    printf("%d\n",b);
    
    swap(pa,pb);
    
    printf("%p\n",pa);
    printf("%p\n",pb);
    
    printf("%d\n",a);
    printf("%d\n",b);
}
```


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

Explain "volatile". 

Can we use "const" and "volatile" in the same variable? 

Can we use "volatile" in a pointer?

<br/>

# 19
https://hackmd.io/@sysprog/c-bitwise

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

# 21 考你如何使用bitwise (難)
https://www.geeksforgeeks.org/write-an-efficient-method-to-check-if-a-number-is-multiple-of-3/

Write a code that check the input is a multiple of 3 or not without using division or mod


<br/>

# 22

Explain lvalue and rvalue.


<br/>

# 23 
https://hackmd.io/@Rance/SkSJL_5gX?type=view

https://cvfiasd.pixnet.net/blog/post/273373732-%E5%88%A9%E7%94%A8function-pointer-array%E7%B4%A2%E5%BC%95%E5%87%BD%E5%BC%8F

https://ppt.cc/qNDB
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
https://ppt.cc/qNDB

# 24 (難)

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
[extern / inline / intern](https://hackmd.io/@HsuChiChen/c-inline)

C裡面的memory

程式段(.text)主要存放程式的機器碼，

資料段(.data)則是存放全域變數的資料，

BSS 段(.bss)存放的是未初始化的全域變數，

堆積段(.heap)程式使用 malloc 進行記憶體分配時，可以分配的動態記憶空間

堆疊段(.stack)則存放「參數、函數返回點、區域變數、框架指標」等資料

有出多選題問Stack裡面放什麼資料


<br/>

# 35

What is "const" ? and what is the meaning of:

```
1. const int a;
2. int const a;
3. const int * a;
4. int * const a;
5. int const * a const;
```


<br/>

# 36

What is the difference between "Inline Function" and "Macro" ?


<br/>

# 37
https://www.796t.com/content/1547705175.html

Explain "static" ?


<br/>

# 38
https://nwpie.blogspot.com/2017/05/5-stack-heap.html

https://ptt-chat.com/WomenTalk/l/CHAT.M.1598976583.A.721

What is stack and heap when talking about memory?

<br/>

# 39

Explain "thread" and "process",and what is the difference?

<br/>

# 40

Typedef 在C語言中頻繁用以宣告一個已經存在的資料型態的同義字，也可以用預處理器做類似的事，例如思考一下下面的例子:

```
#define dPS struct s *
typedef struct s * tPS;
```
哪種方法更好?為什麼?

<br/>

# 41
https://www.geeksforgeeks.org/difference-between-definition-and-declaration/

What is the difference between variable declaration and definition?



<br/>

# 42

What is the output of the following program?

```
void foo(void){
	unsigned int a = 6;
	int b = -20;
	(a+b>6) ? puts(">6"): puts("<6");
}
```

<br/>

# 43

The faster way to an integer multiply by 7 ? (bitwise)

<br/>

# 44

以單字為反轉字串， Ex: He is a boy => boy a is He。


<br/>

# 45

計算自訂型態的記憶體大小，不可以使用sizeof，也不可有自訂型態變數或其指標。


<br/>

# 46

Write functions isUpper() and toUpper()


<br/>

# 47

Count the number of 1 in an integer x (in binary)?

<br/>

