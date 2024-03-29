﻿<span id = "jump"></span>
# C++ 指针

标签（空格分隔）： C++


----------
学习 C++ 的指针既简单又有趣。通过指针，可以简化一些 C++ 编程任务的执行，还有一些任务，如动态内存分配，没有指针是无法执行的。所以，想要成为一名优秀的 C++ 程序员，学习指针是很有必要的。

正如您所知道的，每一个变量都有一个内存位置，每一个内存位置都定义了可使用连字号（&）运算符访问的地址，它表示了在内存中的一个地址。请看下面的实例，它将输出定义的变量地址：

```
#include <iostream>
 
using namespace std;
 
int main ()
{
   int  var1;
   char var2[10];
 
   cout << "var1 变量的地址： ";
   cout << &var1 << endl;
 
   cout << "var2 变量的地址： ";
   cout << &var2 << endl;
 
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    var1 变量的地址： 0xbfebd5c0
    var2 变量的地址： 0xbfebd5b6

通过上面的实例，我们了解了什么是内存地址以及如何访问它。接下来让我们看看什么是指针。


----------
## 什么是指针？ ##


指针是一个变量，其值为另一个变量的地址，即，内存位置的直接地址。就像其他变量或常量一样，您必须在使用指针存储其他变量地址之前，对其进行声明。指针变量声明的一般形式为：
```
type *var-name;
```
在这里，type 是指针的基类型，它必须是一个有效的 C++ 数据类型，var-name 是指针变量的名称。用来声明指针的星号 * 与乘法中使用的星号是相同的。但是，在这个语句中，星号是用来指定一个变量是指针。以下是有效的指针声明：
```
int    *ip;    /* 一个整型的指针 */
double *dp;    /* 一个 double 型的指针 */
float  *fp;    /* 一个浮点型的指针 */
char   *ch;    /* 一个字符型的指针 */
```
所有指针的值的实际数据类型，不管是整型、浮点型、字符型，还是其他的数据类型，都是一样的，都是一个代表内存地址的长的十六进制数。不同数据类型的指针之间唯一的不同是，指针所指向的变量或常量的数据类型不同。


----------
## C++ 中使用指针 ##


使用指针时会频繁进行以下几个操作：定义一个指针变量、把变量地址赋值给指针、访问指针变量中可用地址的值。这些是通过使用一元运算符 * 来返回位于操作数所指定地址的变量的值。下面的实例涉及到了这些操作：

```
#include <iostream>
 
using namespace std;
 
int main ()
{
   int  var = 20;   // 实际变量的声明
   int  *ip;        // 指针变量的声明
 
   ip = &var;       // 在指针变量中存储 var 的地址
 
   cout << "Value of var variable: ";
   cout << var << endl;
 
   // 输出在指针变量中存储的地址
   cout << "Address stored in ip variable: ";
   cout << ip << endl;
 
   // 访问指针中地址的值
   cout << "Value of *ip variable: ";
   cout << *ip << endl;
 
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Value of var variable: 20
    Address stored in ip variable: 0xbfc601ac
    Value of *ip variable: 20


----------
## C++ 指针详解 ##


在 C++ 中，有很多指针相关的概念，这些概念都很简单，但是都很重要。下面列出了 C++ 程序员必须清楚的一些与指针相关的重要概念：

概念|	描述
--|:--
[C++ Null 指针](#jump1)|	C++ 支持空指针。NULL 指针是一个定义在标准库中的值为零的常量。
[C++ 指针的算术运算](#jump2)|	可以对指针进行四种算术运算：++、--、+、-
[C++ 指针 vs 数组](#jump3)|	指针和数组之间有着密切的关系。
[C++ 指针数组](#jump4)| 可以定义用来存储指针的数组。
[C++ 指向指针的指针](#jump5)|	C++ 允许指向指针的指针。
[C++ 传递指针给函数](#jump6)|	通过引用或地址传递参数，使传递的参数在调用函数中被改变。
[C++ 从函数返回指针](#jump7)|	C++ 允许函数返回指针到局部变量、静态变量和动态内存分配。


<span id = "jump1"></span>
# C++   Null 指针#
[<i class="icon-arrow-left"></i>C++ 指针](#jump)
在变量声明的时候，如果没有确切的地址可以赋值，为指针变量赋一个 NULL 值是一个良好的编程习惯。赋为 NULL 值的指针被称为空指针。

NULL 指针是一个定义在标准库中的值为零的常量。请看下面的程序：
```
#include <iostream>

using namespace std;

int main ()
{
   int  *ptr = NULL;

   cout << "ptr 的值是 " << ptr ;
 
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    ptr 的值是 0

在大多数的操作系统上，程序不允许访问地址为 0 的内存，因为该内存是操作系统保留的。然而，内存地址 0 有特别重要的意义，它表明该指针不指向一个可访问的内存位置。但按照惯例，如果指针包含空值（零值），则假定它不指向任何东西。

如需检查一个空指针，您可以使用 if 语句，如下所示：
```
if(ptr)     /* 如果 ptr 非空，则完成 */
if(!ptr)    /* 如果 ptr 为空，则完成 */
```
因此，如果所有未使用的指针都被赋予空值，同时避免使用空指针，就可以防止误用一个未初始化的指针。很多时候，未初始化的变量存有一些垃圾值，导致程序难以调试。
[<i class="icon-arrow-left"></i>C++ 指针](#jump)


<span id = "jump2"></span>
# C++  指针的算术运算#
[<i class="icon-arrow-left"></i>C++ 指针](#jump)
指针是一个用数值表示的地址。因此，您可以对指针执行算术运算。可以对指针进行四种算术运算：++、--、+、-。

假设 ptr 是一个指向地址 1000 的整型指针，是一个 32 位的整数，让我们对该指针执行下列的算术运算：

```
ptr++
```
在执行完上述的运算之后，ptr 将指向位置 1004，因为 ptr 每增加一次，它都将指向下一个整数位置，即当前位置往后移 4 个字节。这个运算会在不影响内存位置中实际值的情况下，移动指针到下一个内存位置。如果 ptr 指向一个地址为 1000 的字符，上面的运算会导致指针指向位置 1001，因为下一个字符位置是在 1001。

## 递增一个指针 ##
我们喜欢在程序中使用指针代替数组，因为变量指针可以递增，而数组不能递增，因为数组是一个常量指针。下面的程序递增变量指针，以便顺序访问数组中的每一个元素：

```
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int  *ptr;
 
   // 指针中的数组地址
   ptr = var;
   for (int i = 0; i < MAX; i++)
   {
      cout << "Address of var[" << i << "] = ";
      cout << ptr << endl;
 
      cout << "Value of var[" << i << "] = ";
      cout << *ptr << endl;
 
      // 移动到下一个位置
      ptr++;
   }
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Address of var[0] = 0xbfa088b0
    Value of var[0] = 10
    Address of var[1] = 0xbfa088b4
    Value of var[1] = 100
    Address of var[2] = 0xbfa088b8
    Value of var[2] = 200

## 递减一个指针 ##
同样地，对指针进行递减运算，即把值减去其数据类型的字节数，如下所示：

```
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int  *ptr;
 
   // 指针中最后一个元素的地址
   ptr = &var[MAX-1];
   for (int i = MAX; i > 0; i--)
   {
      cout << "Address of var[" << i << "] = ";
      cout << ptr << endl;
 
      cout << "Value of var[" << i << "] = ";
      cout << *ptr << endl;
 
      // 移动到下一个位置
      ptr--;
   }
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Address of var[3] = 0xbfdb70f8
    Value of var[3] = 200
    Address of var[2] = 0xbfdb70f4
    Value of var[2] = 100
    Address of var[1] = 0xbfdb70f0
    Value of var[1] = 10

## 指针的比较 ##
指针可以用关系运算符进行比较，如 ==、< 和 >。如果 p1 和 p2 指向两个相关的变量，比如同一个数组中的不同元素，则可对 p1 和 p2 进行大小比较。

下面的程序修改了上面的实例，只要变量指针所指向的地址小于或等于数组的最后一个元素的地址 &var&#91;MAX - 1]，则把变量指针进行递增：

```
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int  *ptr;
 
   // 指针中第一个元素的地址
   ptr = var;
   int i = 0;
   while ( ptr <= &var[MAX - 1] )
   {
      cout << "Address of var[" << i << "] = ";
      cout << ptr << endl;
 
      cout << "Value of var[" << i << "] = ";
      cout << *ptr << endl;
 
      // 指向上一个位置
      ptr++;
      i++;
   }
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Address of var[0] = 0xbfce42d0
    Value of var[0] = 10
    Address of var[1] = 0xbfce42d4
    Value of var[1] = 100
    Address of var[2] = 0xbfce42d8
    Value of var[2] = 200 

[<i class="icon-arrow-left"></i>C++ 指针](#jump)


<span id = "jump3"></span>
# C++  指针 vs 数组#
[<i class="icon-arrow-left"></i>C++ 指针](#jump)
指针和数组是密切相关的。事实上，指针和数组在很多情况下是可以互换的。例如，一个指向数组开头的指针，可以通过使用指针的算术运算或数组索引来访问数组。请看下面的程序：

```
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int  *ptr;
 
   // 指针中的数组地址
   ptr = var;
   for (int i = 0; i < MAX; i++)
   {
      cout << "var[" << i << "]的内存地址为 ";
      cout << ptr << endl;
 
      cout << "var[" << i << "] 的值为 ";
      cout << *ptr << endl;
 
      // 移动到下一个位置
      ptr++;
   }
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    var[0]的内存地址为 0x7fff59707adc
    var[0] 的值为 10
    var[1]的内存地址为 0x7fff59707ae0
    var[1] 的值为 100
    var[2]的内存地址为 0x7fff59707ae4
    var[2] 的值为 200

然而，指针和数组并不是完全互换的。例如，请看下面的程序：

```
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
 
   for (int i = 0; i < MAX; i++)
   {
      *var = i;    // 这是正确的语法
      var++;       // 这是不正确的
   }
   return 0;
}
```
把指针运算符 * 应用到 var 上是完全可以的，但修改 var 的值是非法的。这是因为 var 是一个指向数组开头的常量，不能作为左值。

由于一个数组名对应一个指针常量，只要不改变数组的值，仍然可以用指针形式的表达式。例如，下面是一个有效的语句，把 var[2] 赋值为 500：
```
*(var + 2) = 500;
```
上面的语句是有效的，且能成功编译，因为 var 未改变。
[<i class="icon-arrow-left"></i>C++ 指针](#jump)


<span id = "jump4"></span>
# C++   指针数组#
[<i class="icon-arrow-left"></i>C++ 指针](#jump)
在我们讲解指针数组的概念之前，先让我们来看一个实例，它用到了一个由 3 个整数组成的数组：

```
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
 
   for (int i = 0; i < MAX; i++)
   {
      cout << "Value of var[" << i << "] = ";
      cout << var[i] << endl;
   }
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Value of var[0] = 10
    Value of var[1] = 100
    Value of var[2] = 200

可能有一种情况，我们想要让数组存储指向 int 或 char 或其他数据类型的指针。下面是一个指向整数的指针数组的声明：
```
int *ptr[MAX];
```
在这里，把 **ptr** 声明为一个数组，由 MAX 个整数指针组成。因此，ptr 中的每个元素，都是一个指向 int 值的指针。下面的实例用到了三个整数，它们将存储在一个指针数组中，如下所示：

```
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int *ptr[MAX];
 
   for (int i = 0; i < MAX; i++)
   {
      ptr[i] = &var[i]; // 赋值为整数的地址
   }
   for (int i = 0; i < MAX; i++)
   {
      cout << "Value of var[" << i << "] = ";
      cout << *ptr[i] << endl;
   }
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Value of var[0] = 10
    Value of var[1] = 100
    Value of var[2] = 200

您也可以用一个指向字符的指针数组来存储一个字符串列表，如下：

```
#include <iostream>
 
using namespace std;
const int MAX = 4;
 
int main ()
{
 const char *names[MAX] = {
                   "Zara Ali",
                   "Hina Ali",
                   "Nuha Ali",
                   "Sara Ali",
   };
 
   for (int i = 0; i < MAX; i++)
   {
      cout << "Value of names[" << i << "] = ";
      cout << names[i] << endl;
   }
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Value of names[0] = Zara Ali
    Value of names[1] = Hina Ali
    Value of names[2] = Nuha Ali
    Value of names[3] = Sara Ali
[<i class="icon-arrow-left"></i>C++ 指针](#jump)


<span id = "jump5"></span>
# C++  指向指针的指针（多级间接寻址）#
[<i class="icon-arrow-left"></i>C++ 指针](#jump)
指向指针的指针是一种多级间接寻址的形式，或者说是一个指针链。通常，一个指针包含一个变量的地址。当我们定义一个指向指针的指针时，第一个指针包含了第二个指针的地址，第二个指针指向包含实际值的位置。

C++ 中指向指针的指针
一个指向指针的指针变量必须如下声明，即在变量名前放置两个星号。例如，下面声明了一个指向 int 类型指针的指针：
```
int **var;
```
当一个目标值被一个指针间接指向到另一个指针时，访问这个值需要使用两个星号运算符，如下面实例所示：

```
#include <iostream>
 
using namespace std;
 
int main ()
{
    int  var;
    int  *ptr;
    int  **pptr;
 
    var = 3000;
 
    // 获取 var 的地址
    ptr = &var;
 
    // 使用运算符 & 获取 ptr 的地址
    pptr = &ptr;
 
    // 使用 pptr 获取值
    cout << "var 值为 :" << var << endl;
    cout << "*ptr 值为:" << *ptr << endl;
    cout << "**pptr 值为:" << **pptr << endl;
 
    return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    var 值为 :3000
    *ptr 值为:3000
    **pptr 值为:3000
    
[<i class="icon-arrow-left"></i>C++ 指针](#jump)


<span id = "jump6"></span>
# C++  传递指针给函数#
[<i class="icon-arrow-left"></i>C++ 指针](#jump)
C++ 允许您传递指针给函数，只需要简单地声明函数参数为指针类型即可。

下面的实例中，我们传递一个无符号的 long 型指针给函数，并在函数内改变这个值：

```
#include <iostream>
#include <ctime>
 
using namespace std;
void getSeconds(unsigned long *par);
 
int main ()
{
   unsigned long sec;
 
 
   getSeconds( &sec );
 
   // 输出实际值
   cout << "Number of seconds :" << sec << endl;
 
   return 0;
}
 
void getSeconds(unsigned long *par)
{
   // 获取当前的秒数
   *par = time( NULL );
   return;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Number of seconds :1294450468

能接受指针作为参数的函数，也能接受数组作为参数，如下所示：

```
#include <iostream>
using namespace std;
 
// 函数声明
double getAverage(int *arr, int size);
 
int main ()
{
   // 带有 5 个元素的整型数组
   int balance[5] = {1000, 2, 3, 17, 50};
   double avg;
 
   // 传递一个指向数组的指针作为参数
   avg = getAverage( balance, 5 ) ;
 
   // 输出返回值
   cout << "Average value is: " << avg << endl; 
    
   return 0;
}
 
double getAverage(int *arr, int size)
{
  int    i, sum = 0;       
  double avg;          
 
  for (i = 0; i < size; ++i)
  {
    sum += arr[i];
   }
 
  avg = double(sum) / size;
 
  return avg;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    Average value is: 214.4
    
[<i class="icon-arrow-left"></i>C++ 指针](#jump)



<span id = "jump7"></span>
# C++  从函数返回指针#
[<i class="icon-arrow-left"></i>C++ 指针](#jump)
在上一章中，我们已经了解了 C++ 中如何从函数返回数组，类似地，C++ 允许您从函数返回指针。为了做到这点，您必须声明一个返回指针的函数，如下所示：
```
int * myFunction()
{
.
.
.
}
```
另外，C++ 不支持在函数外返回局部变量的地址，除非定义局部变量为 static 变量。

现在，让我们来看下面的函数，它会生成 10 个随机数，并使用表示指针的数组名（即第一个数组元素的地址）来返回它们，具体如下：
```
#include <iostream>
#include <ctime>
#include <cstdlib>
 
using namespace std;
 
// 要生成和返回随机数的函数
int * getRandom( )
{
  static int  r[10];
 
  // 设置种子
  srand( (unsigned)time( NULL ) );
  for (int i = 0; i < 10; ++i)
  {
    r[i] = rand();
    cout << r[i] << endl;
  }
 
  return r;
}
 
// 要调用上面定义函数的主函数
int main ()
{
   // 一个指向整数的指针
   int *p;
 
   p = getRandom();
   for ( int i = 0; i < 10; i++ )
   {
       cout << "*(p + " << i << ") : ";
       cout << *(p + i) << endl;
   }
 
   return 0;
}
```
当上面的代码被编译和执行时，它会产生下列结果：

    624723190
    1468735695
    807113585
    976495677
    613357504
    1377296355
    1530315259
    1778906708
    1820354158
    667126415
    *(p + 0) : 624723190
    *(p + 1) : 1468735695
    *(p + 2) : 807113585
    *(p + 3) : 976495677
    *(p + 4) : 613357504
    *(p + 5) : 1377296355
    *(p + 6) : 1530315259
    *(p + 7) : 1778906708
    *(p + 8) : 1820354158
    *(p + 9) : 667126415
    
[<i class="icon-arrow-left"></i>C++ 指针](#jump)
