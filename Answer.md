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

發現總共有8個func，因此2^8 = 256
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

1. An integer
2. A pointer to an integer
3. A pointer to a pointer to an integer
4. An array of 10 integers
5. An array of 10 pointers to integers
6. A pointer to an array of 10 integers
7. A pointer to a function that takes an integer as an argument and returns an integer
8. An array of ten pointers to functions that take an integer argument and return an integer

// 寫出上述所述之指標

//(用英文比較好理解)
Ans:

1. int p;
2. int *p;
3. int **p;
4. int p[10];
5. int *p[10];
6. int (*p)[10];
7. int (*p)(int);
8. int (*p[10])(int);


<br/>

# 14 Swap 的各種寫法 (bitwise ,指標)

[bitwise解法](http://puremonkey2010.blogspot.com/2011/05/c-bitwise-operation.html)

Ans:
```
void swap1(int* a, int* b){

    *a = *a^*b;
    *b = *a^*b;
    *a = *a^*b;
}

int main()
{
    void swap(int*, int*);
    int a =10;
    int b =20;
    int* pa =&a;
    int* pb =&b;

    printf("%d\n",a);
    printf("%d\n",b);

    swap1(pa,pb);

    printf("%d\n",a);
    printf("%d\n",b);

    return 0;
}

```

[指標解法](https://www.796t.com/content/1549322654.html)

Ans:
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


Ans:
```
#include <stdio.h>
#define MAX(a,b) (a)>(b)?(a):(b)

int maxSubArray(int* nums, int numsSize){

    int i=0;
    int best = INT_MIN; //假如 [-1,-2,-3]，總和還是<0 因此不能設為零，因此設成INT_MIN。
    int sum = 0;

    for(i =0;i<=numSize;i++){

        best = MAX(sum +nums[i],nums[i]);
        sum = MAX(best,sum);
    }
    return 0;
}
```
<br/>

# 16

https://mkfsn.blogspot.com/2016/12/blog-post.html

Explain "#error"

Ans:

error 是一種Macro，在compiler執行時，若有遇到問題，就會終止程式，並且輸出錯誤訊息。

<br/>

# 17
Explain "struct" and "union"?

Ans:

struct 與 union 很像，但最大的不同點是所使用的空間，

假設分別宣告一個struct 以及 union

struct A{
    int a;
    double;
}

union A{
    int a;
    double;
}

struct A 所佔據的空間為 4+8 =12 byte;

union A 所佔據的空間為最大的參數為 8 byte;


<br/>

因此，
struct每個參數都是獨立的，都各自佔有記憶體空間，

union內的參數所佔據的空間是共享的，由最大的那個決定大小


<br/>

# 18

Explain "volatile".

Can we use "const" and "volatile" in the same variable?

Can we use "volatile" in a pointer?


Ans:

1.volatile，中文為易揮發的，在c語言中主要是通知compiler不要對進行最佳化，因為他的值會不穩定一直變動。

2.可以同時使用 const,volatile，const所代表的是只可以讀的(Read-only)，因此兩者不衝突。

3.可以，但volatile pointer實際值會變動。

<br/>

# 19
https://hackmd.io/@sysprog/c-bitwise

write a code

a. set the specific bit

b. clear the specific bit

c. inverse the specific bit (0->1; 1->0)


Ans:

```
//a. set the specific bit

#define setbit(a,n) (a |= (1<<(n))


//b. clear the specific bit

#define clearbit(a,n) (a &= ~(1<<(n))


//c. inverse the specific bit (0->1; 1->0)

#define togglebit(a,n) (a ^= (1<<(n))


```
<br/>

# 20
Fill the blank
```
void(*(*papf)[3])(char *); // Rewrite this
typedef ___________;
pf(*papf)[3];
```


Ans:

void(*(*papf)[3])(char *) => pf(*papf)[3];

假設(*papf)[3] = A;

void(*(A)(char *) => pf(A)

因此，typedef void(*pf)(char *);


<br/>

# 21 考你如何使用bitwise (難)
https://www.geeksforgeeks.org/write-an-efficient-method-to-check-if-a-number-is-multiple-of-3/

Write a code that check the input is a multiple of 3 or not without using division or mod

Ans:
```
#include <stdio.h>

void main() {
    int x;
    scanf("%d", &x);

    while(x>=3){
        x=x-3;

        if(x<3 && x==0){
            printf("x = %d 這是3的倍數\n", x);
        }
        else if(x<3&& x!=0){
            printf("x = %d 這不是3的倍數\n", x);
        }
    }
}

```
<br/>

# 22

Explain lvalue and rvalue.

Ans:

lvalue 等號左側的值，有實際記憶體位置，可以使用reference

rvalue 等號右側的值，單純給值，不可使用reference

<br/>

# 23
https://hackmd.io/@Rance/SkSJL_5gX?type=view

https://cvfiasd.pixnet.net/blog/post/273373732-%E5%88%A9%E7%94%A8function-pointer-array%E7%B4%A2%E5%BC%95%E5%87%BD%E5%BC%8F

https://ppt.cc/qNDB  //(參考這寫法)
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

Ans:

```
int main(int n) {
    static void (*x[5])(void) = {
        [1] = func1,
        [2] = func2,
        [3] = func3,
        [4] = func4,
        [5] = func5
    };
    x[(n%5)+1]();
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

Ans:

```
extern void func1(void);
extern void f2(void);
extern void f3(void);
extern void f4(void);
extern void f5(void);

int main(int n) {
    static void (*x[16])(void) = {
        [1] = f1,
        [3] = f2,
        [4] = f3,
        [7] = f4,
        [15] = f5
    };
    x[n % 16]();
}
```


<br/>

# 25
寫一個 function 可傳入正整數參數 N，回傳 1 + 2 + 3 +…+N 的和

Ans:

```
void SUM(int n){
    return (1+n)*(n)/2;
}
```
<br/>

# 26  寫出反轉字元的方式

reverse a string

<br/>

# 27

寫一個“標準”巨集MIN ，這個巨集輸入兩個參數並返回較小的一個。

Ans:

```
#define MIN(a,b) (a)<(b)?(a):(b)
```
<br/>

# 28
Write a MARCO to calculate the square of integer a.

Ans:

```
#define square(a) ((a)*(a))
```

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

Ans:

ival => Int

**p => a pointer to a pointer to a integer

*p  => a pointer to a integer

所以，Ival = *p 會出現錯誤

<br/>

# 32
What is the possible error of below SQR function.

```
int SQR(volatile int *a){
   return (*a)*(*a);
}
```

Ans:

因為是 volatile int* a ，所以不穩定數值可能會變，

因此，2個*a的值可能會不同。

```
//正確寫法

int SQR(volatile int *a){
    int b;
    b = *a;
   return (b)*(b);
}
```

<br/>

# 33
用預處理指令#define 聲明一個常數，用以表明1年中有多少秒（忽略閏年問題）

Ans:

```
//記得要空格

#define leapyearsec (60*60*24*365)

//應該也可以寫成下面這樣

#define leapyearsec() (60*60*24*365)
```
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

Ans:

// 注意const 在 * 的左方還是右方，以這題為例，*左方修飾int,*右方修飾指標

1. const int a; => 只可以讀的整數a
2. int const a; => 只可以讀的整數a
3. const int * a; =>指標a指向一個只可以讀的整數,指標可以改,a不能改
4. int * const a; =>一個只可以讀的指標a指向一個整數 ,指標不能改，但指向的整數可以改
5. int const * a const; => 一個只可以讀的指標a指向一個只可以讀的整數，都不能改

<br/>

# 36

What is the difference between "Inline Function" and "Macro" ?

Ans:

Inline Function 代表的是最佳化函式，inline告訴compiler要執行最佳化，因此會在程式中展開，若是一般的Function要從外部讀取比較花時間。

Macro 是指在預處理器就先執行的巨集，在程式中只執行單純的替換文本的功能。

<br/>

# 37
https://www.796t.com/content/1547705175.html

Explain "static" ?

Ans:

static主要的功能是隱藏global，讓他只能在特定範圍內可見，若兩個檔案皆有相同的宣告變數時，可透過此方法使其執行時正常。此外static的作用是預設初始化為0


<br/>

# 38
https://nwpie.blogspot.com/2017/05/5-stack-heap.html

https://ptt-chat.com/WomenTalk/l/CHAT.M.1598976583.A.721

What is stack and heap when talking about memory?


Ans:

stack 用於靜態記憶體配置，是拿來給程式呼叫 function 時存放 function 資料用的。

heap 用於動態記憶體配置，用來存放並且管理，程式全部所需要用到的變數與資料。

<br/>

# 39

https://www.geeksforgeeks.org/difference-between-process-and-thread/

Explain "thread" and "process",and what is the difference?

Ans:

process : 進程，以電腦為例，每個軟體都是一個process，每個process會去share總共的cpu/memory空間，抓下來後獨自使用不分享，執行時較慢，效率較低。

thread : 每個process裡面至少有一個thread，thread會去分享"process所佔下來的空間"，每個thread一起分享使用這個空間，執行時較快，效率較高。

<br/>

# 40

https://www.runoob.com/note/24230

Typedef 在C語言中頻繁用以宣告一個已經存在的資料型態的同義字，也可以用預處理器做類似的事，例如思考一下下面的例子:

```
#define dPS struct s *
typedef struct s * tPS;
```
哪種方法更好?為什麼?


Ans:

假設，
```
dPS p1,p2;
tPS p3,p4;

//解析後

struct s *p1,p2
tPS p3,p4;
```
p1為指向一個結構的指標，p2只是單純一個結構，p3,p4則都是指向結構的指標，因此使用typedef會比較好。

使用typedef struct s * tPS 更好


<br/>

# 41
https://www.geeksforgeeks.org/difference-between-definition-and-declaration/

What is the difference between variable declaration and definition?

Ans:

舉例來說 :

```
int a ; //declaration
a = 5 ; // definition

declaration:告訴 compiler 我要宣告一個整數型別的a，此時尚未分配記憶體位置 ，一個變量或函數可以多次宣告。


definition: 告訴 compiler 我要將5放入a的裡面，此時會分配記憶體位置，一個變量或函數只能定義一次。

```

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

Ans:

unsigned int 與 int 比較或是進行運算時 ，會都變成unsigned形式，因此都會變成正數。

所以會輸出puts(">6")

<br/>

# 43

The faster way to an integer multiply by 7 ? (bitwise)


Ans:

```
n = (n<<3) + n

n = (n<<2) + (n<<1) + (n<<0)
```
<br/>

# 44 leetcode 151

https://leetcode.com/problems/reverse-words-in-a-string/discuss/805248/C-4ms-and-5.7M-in-place-no-string-library.

https://leetcode.com/problems/reverse-words-in-a-string/discuss/1531349/Two-pointers-solution-in-C
以單字為反轉字串， Ex: He is a boy => boy a is He。


<br/>

# 45

計算自訂型態的記憶體大小，不可以使用sizeof，也不可有自訂型態變數或其指標。


<br/>

# 46

Write functions isUpper() and toUpper()

Ans:

```
#include <stdbool.h>

bool isUpper(int n){
    return (n >='A' && n<='Z');
}

int toUpper(int n){

    if(isUpper(n)){
        retuen n;
    }
    else{
        return(n+'A'-'a');
    }
}
```


<br/>

# 47

Count the number of 1 in an integer x (in binary)?

Ans:

```
void main(){

    int x;
    scanf("%d",&x);

    int c=0;

    while(x!=0){
        c = c + 1;
        x= x&(x-1);
    }
    printf("總共有%d個1\n",c);
}
```
<br/>


# 48

印出 

```
*
***
*****
```

Ans:

```
//先理出這個思路
#include <stdio.h>

int main()
{
    int i, j, n;

    /* Input number of rows from user */
    printf("Enter value of n: ");
    scanf("%d", &n);

    for(i=1; i<=n; i++)
    {
        /* Print i number of stars */
        for(j=1; j<=i; j++)
        {
            printf("*");
        }

        /* Move to next line */
        printf("\n");
    }

    return 0;
}
```

```
#include <stdio.h>

int main()
{
    int i, j, n;

    /* Input number of rows from user */
    printf("Enter value of n: ");
    scanf("%d", &n);

    for(i=1; i<=n; i+=2)
    {
        /* Print i number of stars */
        for(j=1; j<=i; j++)
        {
            printf("*");
        }

        /* Move to next line */
        printf("\n");
    }

    return 0;
}
```