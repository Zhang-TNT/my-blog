# DataStructure_tutorial
> Data Structure tutorial for C

## Introduction

> 计算机解决一个具体问题：从具体问题抽象出一个适当的数学模型；设计一个解此数学模型的算法；编写程序，测试、调整直至得到最终解答

1. 数学知识复习

    证明数据结构分析中结论的两个常用方法是**归纳法**和**反证法**。

    + 归纳法

        第一步证明*基准情况*，对于小群体事件的正确性；第二步进行*归纳假设*；第三步使用这个假设对下一个值进行证明。

    + 反证法

        反证法是通过假设定理不成立，然后证明该假设导致某个已知的性质不成立，从而说明原假设是错误的。

2. 递归

    有时候数学函数以不太标准的形式来定义，当一个函数用它自己来定义时就称为**递归（recursive）**，递归调用将反复进行直到基准情形出现。递归的四个基本法则

    + 基准情形

        基准情形不用递归就能求解

    + 不断推进

        递归调用总朝着基准情形方向推进

    + 设计法则

        假设所有递归调用都能运行

    + 合成效益法则

        在求解一个问题的同一实例时，切勿在不同的递归调用中做重复性工作

    案例1. 递归方法求阶乘$n!$

    数学分析：若$f(n)$表示$n!$，则满足$f(n) = n\times f(n-1)$，基准情形是$n=0$或$n=1$时，$f(n)=1$。代码实现如下

    ```c
    int my_factorial(int len)
    {
        int result = 0;
        if (len < 0)
        {
            return -1;
        }
        else if (len == 0 || len == 1)
        {
            return 1;
        }
        else
        {
            result = len * my_factorial(len - 1);
        }
        return result;
    }
    ```

    案例2. 有5各学生坐一起，问第5个学生年龄，说其比第4个大2岁；问第4个年龄，说其比第3个大2岁；问第3个年龄，说其比第2个大2岁；问第2个年龄，说其比第1个大2岁；问第1个年龄，说其10岁。求第5个学生年龄

    数学分析：若$f(n)$表示第$n$个学生的年龄，则满足$f(n)=f(n-1)+2$，基准情形是$n=1$时，$f(n)=10$。代码实现如下

    ```c
    int my_ageFactorial(int len)
    {
        int result = 0;
        if (len <= 0)
        {
            return -1;
        }
        else if (len == 1)
        {
            return 10;
        }
        else
        {
            result = my_ageFactorial(len - 1) + 2;
        }
        return result;
    }
    ```

3. 编程机制

    C编程的基本策略是，用程序把源代码文件转换为可执行文件，即**编译**和**链接**。编译器把源代码转换为目标代码（`.obj`），链接器把中间代码和其他代码合并，生成可执行文件（`.exe`），目标文件和可执行文件都由机器语言指令组成。

## Review

### 2.1 数据和C

1. 常量

    数据类型在程序使用之前就预先设定好，在整个程序的运行过程中没有变化，称为**常量**（constant），在常量末尾加专用字符，强制指定常量类型，例如`3.14159f`，`31415U`，`10LU`等。有以下几种

    + 整形常量

        整数是没有小数部分的数。

    + 实型常量

        实型是带有小数部分的数。计算机把实数分为**小数部分**和**指数部分**来表示，两种表示方法

        + 小数形式：`3.1415`
        + 指数形式：`e`或`E`表示底数10，前后必须有数字，且后面必须为整数，`3.16E2`表示`316`。

    + 字符常量

        普通字符：用单引号括起来的一个字符，本质是`int`型的ASCII码

        转义字符：以`\`开头的字符

    + 字符串常量

        用双引号把若干个字符常量括起来

    + 符号常量

        用`#define`指令，指定用一个符号名称代表一个常量，符号常量**不占内存**，只是一个临时符号，代表一个值，在预编译后这个符号就不存在了，符号常量用大写字母表示。

2. 变量

    数据类型在程序的运行过程中会被改变或被赋值，称为**变量**（variable），变量必须**先定义初始化后使用**，变量名实际上是以一个名字代表的一个存储地址，未赋值的变量的值由编译器决定。有以下几种

    + 整型变量

        关键字`int`，一般占4个字节，`short`比`int`占用的内存少，`long`比`int`占用的内存多。提供附属关键字`short`、`long`、`long long`和`unsigned`。在打印时，`unsigned int`使用转义字符`%u`；`long`使用转义字符`%ld`；十六进制使用转义字符`%x`或`%#x`；八进制使用转义字符`%o`或`%#o`；内存地址使用转义字符`%p`。

    + 实型变量

        关键字`float`，一般占4个字节，`double`比`float`占用内存多，实型的表示类似科学计数法，指数计数法。提供附属关键字`double`和`long double`。在使用指数计数法时，`e`的两侧必须有数字，且右侧必须为整数，例如`float num = 6.63e-3;`。在打印时，转换说明`%f`为十进制计数法打印；转换说明`%e`为指数计数法打印。`NaN`为浮点类型。实型数据不能加修饰符`signed`或`unsigned`。

    + 字符变量

        关键字`char`，一般占1个字节，`char`类型用于存储字符，但技术层面`char`是整型，`char`实际上存储的是整型，即ASCII码，65代表`A`，97代表`a`。`char`被定义为8位的存储单元，在初始化时使用单引号`''`进行赋值，使用转换说明`%c`进行字符打印。

    + 常变量

        在定义变量时，加关键字`const`，常变量**所在期间其值不能改变**，有类型并且占内存。

3. 存储方式

   + 常量
   
       常量的存储位置可分为**只读数据段**、**代码段**、**栈**和**数据段**这几种情况。
   
       + 只读数据段：常量、`const`全局常量等，只读
       + 代码段：存储程序的机器指令
       + 栈：局部`const`变量，动态分配的内存区域
       + 数据段：非常量变量于此存储
   
       字面常量存储在只读数据段或代码段；`#define`常量不占用存储空间；`const`全局常量在只读数据段，`const`局部常量在栈中；字符串常量在只读数据段。
   
   + 变量
   
       变量的存储方式可分为**静态存储方式**和**动态存储方式**。
   
       + 静态：由系统分配
       + 动态：开发者进行动态分配
   
4. 存储类别

    C语言有以下关键字作为存储类别说明符：`auto`、`register`、`static`、`extern`、`_Thread_local`。

    + `auto`：由系统管理分配内存，只能用于块作用域的变量声明中，一般可以省略关键字

    + `register`：将变量归为寄存器存储类别，以最快速度访问，同时地址不被释放

    + `static`：用于块作用域声明，能保留其存储单元不被释放，但是只有在执行块内的代码时才能访问；且由于静态存储长期占用内存不释放降低了程序效率，同时调用多次后的当前值往往未知；如需对某些外部变量加以限制，只允许在本文件中被引用而不被其他文件引用，可使用关键字`static`对外部变量进行声明；还可用于限制函数的作用域。

    + `extern`：作为扩展作用域使用，如下

        + 在一个文件内扩展外部变量的作用域

            在定义点之前的函数引用外部变量，需要在引用之前使用关键字`extern`对该变量作**外部变量声明**，案例如下

            ```c
            int main()
            {
                extern int a, b, c;	// 把外部变量a, b, c作用域扩展至此
                return 0;
            }
            int a, b, c;	// 定义外部变量a, b, c
            ```

        + 将外部变量的作用域扩展到其他文件

            工程中其他文件如引用当前文件中的外部变量，需要在其他文件中使用关键字`extern`对当前文件中的外部变量作**外部变量声明**，案例如下

            ```c
            // file1.c
            int A;
            int main()
            {
                return 0;
            }
            
            // file2.c
            extern int A;	// 将file1.c中的外部变量A作用域扩展至此
            func()
            {
                int a = A;
            }
            ```

            关键字`extern`还可用于扩展函数的作用域。

    + `_Thread_local`：定义线程局部存储

    根据函数能否被其他源文件调用，可将函数分为**内部函数**和**外部函数**

    + 内部函数

        只能被本文件中的其他函数所调用，在定义时添加关键字`static`进行静态声明

    + 外部函数

        可供其他文件调用，在定义时添加关键字`extern`进行外部声明

    查找内存地址，可使用`&`运算符，使用转义字符`%p`进行打印，以十六进制形式表示。

5. 类型限定符

    通常用类型和存储类别来描述一个变量，恒常性、易变形、严格性和原子性，分别用关键字`const`、`volatility`、`restrict`和`_Atomic`声明。

    + `const`：限定变量为只读
    + `volatile`：告诉编译器该变量的值可能会在程序之外被修改，因此编译器不应对其进行优化
    + `restrict`：允许编译器优化某部分代码以更好地支持计算，只能用于指针，表明该指针是访问数据对象的唯一且初始的方式
    + `_Atomic`：确保对变量的操作是不可分割的，在多线程环境下要么完全执行，要么完全不执行，不会被打断，可避免竞争条件，多线程同时访问和修改共享变量时。

### 2.2 数组

1. 一维数组

    数组是按顺序存储的一系列类型相同的值，从0开始索引，使用方括号表面元素个数，大括号表明所含元素，一般使用符号常量表示数组大小，**在定义数组时，必须指定数组大小**。这里举冒泡排序算法为例

    ```c
    // 每次将相邻两个进行比较，然后移位
    void my_bubbleSort(int *arr, int len)
    {
        int temp = 0;
        for (int i = 0; i < len - 1; i++)
        {
            for (int j = 0; j < len - i - 1; j++)
            {
                if (arr[j] > arr[j + 1])
                {
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }
    ```

    选择法是先将10个数中最小的数与`a[0]`对换；再将剩余9个数中最小的数与`a[1]`对换；依此类推，总共需要9次。用选择法对数据进行排序

    ```c
    void my_selectSort(int *arr, int len)
    {
        int temp = 0, minIndex;
        for (int i = 0; i < len - 1; i++)
        {
            minIndex = i;
            for (int j = i + 1; j < len; j++)
            {
                if (arr[j] < arr[minIndex])
                {
                    minIndex = j;
                }
            }
            temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
    ```

    

2. 多维数组

    二维数组常称为**矩阵**，由行（row）和列（column）的排列形式。C语言中，**不能省略高维的大小说明**。二维数组中元素排列的顺序是按行存放，在内存中先顺序存放第1行的元素，再放第2行的元素，依次存放剩余。多维数组元素在内存中的排列顺序：第一维的下标变化最慢，最右边的下标变化最快。

    案例，气象研究员Tempest Cloud为完成她的研究项目要分析5年内每个月的降 水量数据，她首先要解决的问题是如何表示数据。

    ```c
    void my_rainfall(const float arr[][MONTHS])
    {
        printf("\tYEAR\t RAINFALL(inches)\n");
        float total, subtotal;
        for (int i = 0; i < 5; i++)
        {
            for (int j = 0; j < MONTHS; j++)
                subtotal += arr[i][j];
            total += subtotal;
            printf("\t%5d %10.1f\n", i + 2010, subtotal);
            subtotal = 0;
        }
        printf("The yearly average rainfall is %5.1f inches\n", (total / 5));
        printf("\n");
        printf("MONTHLY AVERAGE RAINFALL\n");
        printf("\tJAN\tFEB\tMAR\tAPR\tMAY\tJUN\tJUL\tAUG\tSEP\tOCT\tNOV\tDEC\n");
        for (int i = 0; i < MONTHS; i++)
        {
            for (int j = 0; j < 5; j++)
                subtotal += arr[j][i];
            printf("\t%.1f", subtotal / 5);
            subtotal = 0;
        }
        printf("\n");
    }
    ```

    

3. 字符数组

    用双引号括起来的内容称为**字符串常量**，不可被更改。字符串是存放在字符型数组中，当元素个数小于数组长度，剩余元素自动定为**空字符**`\0`。字符串以空字符`\0`作为结束标志，由C系统自动添加。使用格式符`%c`输入或输出一个字符，格式符`%s`输入或输出一串字符，在进行字符串的输入时**系统把空格字符作为输入的字符串之间的分隔符**。函数`scanf()`使用格式说明符`%s`时，默认读取直到第一个空白符为止的字符序列，**空格之后的所有字符会留在输入缓冲区中**，这就会导致回车键作为第二次输入。

    字符串处理函数

    + `puts(string)`函数，自带换行符
    + `gets(string)`函数，获取键盘输入字符串
    + `strcat(str1, str2)`函数，把`str2`接到`str1`后面，结果存放在`str1`中。
    + `strcpy(str1, str2)`和`strncpy(str1, str2, n)`函数，把`str2`复制到`str1`中；把`str2`中前`n`各字符复制到`str1`中。
    + `strcmp(str1, str2)`函数，比较`str1`和`str2`，**小写字母比大写字母大**，两者相同时函数值为0；`str1>str2`时，函数值为正整数；`str1<str2`时，函数值为负整数。
    + `strlen(str)`函数，返回字符串的实际长度
    + `strlwr(str)`函数，将字符串中大写字母转换为小写字母
    + `strupr(str)`函数，将字符串中小写字母转换为大写字母

    初始化字符数组和初始化指针指向字符串有区别，如下

    ```c
    char str[] = "Hello World!";
    const char *pstr = "Hello World!";
    // 数组名str是常量，不可进行变量操作，如str++
    // 指针名pstr是变量，可进行变量操作，如pstr++
    
    // 未加const关键字的数组的元素是变量，但数组名是常量
    char *str = "Hello World!";
    str[0] = 'F';               // 字符串常量是不可变的
    printf("Hello World!\n");
    printf("%s\n", str);
    
    char str[] = "Hello World!";
    str[0] = 'F';				// 正常，字符数组元素运行被修改
    printf("%s\n", str);
    ```

    

4. 数组常用操作

    1. + 初始化

            分为两种初始化方式：无初始值、给定初始值。大多数编译系统在未指定初始值的情况下会将数组元素初始化为0。

            ```c
            int *my_arrayInit(int len)
            {
                int *pArr;
                pArr = (int *)malloc(len * sizeof(int));
                for (int i = 0; i < len; i++)
                {
                    pArr[i] = i;
                }
                return pArr;
            }
            ```

        + 访问元素

            数组元素被存储在连续的内存空间中，只需要给定数组内存地址和元素索引即可完成对元素的访问。

            ```C
            // 对元素的访问，时间复杂度为O(1)
            int my_arrayAccess(int *arr, int index)
            {
                return *(arr + index);
            }
            ```

        + 插入元素

            数组元素在内存中是“紧挨着的”，若想在数组中见插入一个元素，需要将该位置及之后的所有元素都向后移动一位，并且数组长度必须足够大。

            ```c
            // 数组元素的插入时间复杂度为O(n)
            void my_arrayInsert(int *arr, int size, int num, int index)
            { // 大小为size的数组，在index位置插入数字num
                for (int i = size - 1; i >= index; i--)
                {
                    arr[i + 1] = arr[i];
                }
                arr[index] = num;
            }
            ```

        + 删除元素

            删除某处索引的元素，需要将该索引之后的所有元素向前移动一位。

            ```c
            // 数组元素的删除时间复杂度为O(n)
            void my_arrayDelete(int *arr, int size, int index)
            {
                for (int i = index; i < size - 1; i++)
                {
                    arr[i] = arr[i + 1];
                }
            }
            ```

        + 遍历元素

            通过索引遍历数组。

            ```c
            void my_arrayTraverse(int *arr, int size)
            {
                for (int i = 0; i < size; i++)
                {
                    printf("%d ", arr[i]);
                }
                printf("\n");
            }
            ```

        + 查找元素

            数组中查找指定元素需要遍历数组，对每轮索引进行判断。

            ```c
            int my_arraySearch(int *arr, int size, int target)
            {
                for (int i = 0; i < size; i++)
                {
                    if (arr[i] == target)
                        return i;
                }
                return -1;
            }
            ```

        + 扩容数组

            复杂的系统环境中，无法保证数组容量的安全扩展，**数组长度一般不可变**。现常用新建立一个更大的数组，将原数组元素按位复制到新数组。

            ```c
            int *my_arrayExtend(int *arr, int size, int enlarge)
            {
                int *pArr;
                pArr = (int *)malloc((size + enlarge) * sizeof(int));
                for (int i = 0; i < size; i++)
                {
                    pArr[i] = arr[i];
                }
                for (int i = size; i < size + enlarge; i++)
                {
                    pArr[i] = 0;
                }
                return pArr;
            }
            ```

    **注意**：在定义了一个数组后，**该数组名是地址，是常量**，不能进行变量操作。字符数组由若干个元素组成，每个元素中放一个字符；而字符指针变量中存放的是地址，指向字符串第1个字符的地址；编译时为字符数组分配若干个存储单元，**为字符指针变量只分配一个存储单元**；指针变量可改变，字符数组名为常量不可改变；**字符数组中的元素可被改变，字符指针指向的字符串常量不可被改变**，`char *p = "hello"; *(p + 2) = 'r'`这种写法错误。

### 2.3 指针

1. 定义

    程序中定义了一个变量，在对程序进行编译时会给这个变量分配内存单元，该内存单元存放变量的值，该内存单元的地址即为变量的位置，**地址指向变量单元**，称地址为**指针**。C语言中的地址包括**位置信息**和其所指向的数据的**类型信息**，亦称为“带类型的地址”。变量地址可使用格式说明符`%p`打印。指针作为函数参数时，传递的是参数的地址，而不是参数的全部内容

    ```c
    int a = 10, b = 20;
    int *a_pointer = &a, *b_pointer = &b; // 定义两个整型指针变量
    printf("original a = %d, b = %d\n", a, b);
    printf("*a_pointer = %d, *b_pointer = %d\n", *a_pointer, *b_pointer);
    
    // 引用指针变量
    int num = 100;
    int *p;
    p = &num;	// 给指针变量p赋值，指向num
    printf("%d\n", *p);	// 引用指针变量指向的变量
    printf("%X\n", p);	// 引用指针变量的值
    
    // 指针变量作函数参数
    void swap(int *p1, int *p2)
    {
        int temp;
        temp = *p1;
        *p1 = *p2;
        *p2 = temp;
    }
    
    // 用数组名、指针作函数参数，下面两种写法等价
    void print_array1(int a[], int len)
    {
        for(int i = 0; i < len; i++) printf("%d\n", a[i]);
    }
    
    void print_array2(int *P, int len)
    {
        for(int i = 0; i < len; i++, p++) printf("%d\n", *p);
    }
    ```

    符号`*`是指针运算符，用于访问指针变量所指向的对象。数组名是该数组首元素的地址，因此可通过指针引用数组。**指针变量的值可以被改变，数组名不可被改变**。

2. 方法

    引用一个数组元素，有以下两种方法

    + 下标法：`p[i]`
    + 指针法：`*(p++)`

    ```c
    // 两种方法遍历数组
    void my_arraySubscript(int arr[5])
    {
        for (int i = 0; i < 5; i++)
            printf("arr[%d] = %d\n", i + 1, arr[i]);
    }
    
    void my_arrayPointer(int arr[5])
    {
        printf("the address of arr is %p\n", arr);
        for (int i = 0; i < 5; i++)
            printf("arr[%d] = %d\n", i + 1, *(arr + i));
        printf("the address of arr is %p\n", arr); // arr仍然是第一个元素的地址
    
        int *pArr = arr;
        printf("the address of pArr is %p\n", pArr);
        for (pArr = arr; pArr < arr + 5; pArr++)
            printf("arr[%d] = %d\n", pArr - arr, *pArr);
        printf("the address of pArr is %p\n", pArr); // pArr已经是最后一个元素的地址
    }
    ```

    

3. 指针与多维数组

    对于多维数组，以二维数组`a[3][4]`为例。

    二维数组名`a`代表的是第一行的起始地址

    那么`a+1`为第二行的起始地址，`a[i]`相当于一个指针，指向第`i`行

    可认为`a`相当于一个双重指针，指向第一行这个数组，`(a+i)`指向第`i`行这个数组

    ```c
    void my_twoDimensionalArray(int arr[3][4])
    {
        printf_s("the array is:\n");
        for (int i = 0; i < 3; i++)
        {
            int temp = 1;
            for (int j = 0; j < 4; j++, temp++)
            {
                printf("%2d ", arr[i][j]);
                if (temp % 4 == 0)
                    printf("\n");
            }
            printf("\n");
        }
        printf("\n");
        printf("**arr = %d\n", **arr);                         // **arr = arr[0][0]，即第一行第一个元素的值
        printf("*(*arr + 1) = %d\n", *(*arr + 1));             // *(*arr + 1) = arr[0][1]，即第一行第二个元素的值
        printf("**(arr + 1) = %d\n", **(arr + 1));             // **(arr + 1) = arr[1][0]，即第二行第一个元素的值
        printf("*(*(arr + 1) + 1) = %d\n", *(*(arr + 1) + 1)); // *(*(arr + 1) + 1) = arr[1][1]，即第二行第二个元素的值
    }
    
    ```

    **注意**：`a[i]`和`a`的区别在于，`a[i]`是一维指针，`a`是二维指针；`a[i]`是指向列元素的，`a`是指向行（一维数组）的。

    + 指向数组元素的指针变量

        ```c
        void my_pointerToArrayElement(int arr[3][4])
        {
            int *pArr = &arr[0][0];	// 指针pArr指向数组第一个元素
            for (pArr; pArr < arr[0] + 12; pArr++)
            {
                if ((pArr - arr[0]) % 4 == 0)
                    printf("\n");
                printf("%2d ", *pArr);
            }
        }
        ```

        

    + 指向由m个元素组成的一维数组的指针变量，即指向一维数组的指针

        例如定义`int (*p)[4];`是一个指向长度为4的`int`型数组，并且只能指向一个包含4个元素的一维数组。

        ```c
        void my_pointerToArray(int arr[3][4])
        {
            int(*pArr)[4] = arr; // 指针pArr指向数组第一行
            for (pArr; pArr < arr + 3; pArr++)
            {
                for (int *eArr = *pArr; eArr < *pArr + 4; eArr++) // 指针eArr指向数组每一行的元素
                    printf("%2d ", *eArr);
                printf("\n");
            }
        }
        ```

        **注意**：不可使用`int **p = arr;`，这是因为`*p`的类型未知，因此要保证指针的**基类型**一致。

    

4. 指针与函数

    函数在定义完后，编译时会被分配一段内存空间，该空间的起始地址即为该函数的入口地址。

    + 指向函数的指针

        **函数名代表函数的起始地址**，函数名就是函数的指针。函数指针可以被用来作为函数参数，接收函数指针的这个函数可以回调函数指针所指向的函数。

        ```c
        int (*p)(int, int);// 定义了一个指向函数的指针变量`p`，该函数类型为整型且有两个整型参数。
        int max(int x, int y);
        int a, b, c;
        p = max;
        c = (*p)(a, b);// 调用函数max()
        
        void Hello_print()
        {
            print("Hello\n");
        }
        
        void func_example(void (*ptr)())// 函数指针作为其参数，ptr指向一个函数，这个函数不带参数、无返回值
        {
            ptr();// 调用ptr所指向的哪个函数
        }
        
        void (*temp_func)();// 定义一个无参、无返回值的函数指针temp_func
        temp_func = Hello_print;
        
        int main()
        {
            func_example(temp_func);// 通过函数func_example()回调Hello_print()
        }
        ```

        

    + 返回指针的函数

        函数返回指针，一般形式`int *fun(int xn, int yn);`，相当于该函数返回一个地址。

    + 指针数组和多重指针

        数组的组成元素均为指针类型，称为**指针数组**，每一个元素都存放一个地址，如`int *p[4];`定义了一个大小为4的**整型指针数组**，适用于**指向若干个字符串**，类似二维数组。案例如下

        ```c
        char *name[] = {"Nancy", "Mia", "Kristin", "Sophia"};	// 每一个元素指向一个字符串
        ```

        指向指针的指针变量，亦称为**多重指针**。一般形式`char **p;`相当于`char*(*p);`，指向指针的指针变量存储的是所指向的指针的地址，相当于嵌套映射。

        ```c
        char **p;
        p = name + 2;				// p指向"Kristin"
        printf("%p\n", *p);			// 输出"Kristin"地址
        printf("%s\n", *p);			// 输出"Kristin"
        printf("%c\n", *(p[2]));	// 输出'i'
        ```

        **注意**：在定义指针时，一定要及时对其进行初始化，否则该指针所指向的内存单元不可预料。

### 2.4 内存分配

当声明一个数据类型时，其所需的内存在编译时就被分配，在离开其作用域后内存自动释放。由于在声明数组时，必须指定数组长度使用动态内存分配在运行时为其分配内存。对内存的动态分配有以下库函数

+ 用`void *malloc(unsigned int size);`开辟动态存储区

    在内存中动态存储区中分配一个长度为`size`**连续空间**，返回所分配区域的第一个字节的地址，分配失败则返回空指针（NULL）。

+ 用`void *calloc(unsigned n, unsigned size);`开辟动态存储区

    在内存的动态存储区中分配`n`个长度为`size`的连续空间，一般用于保存数组，即**动态数组**。返回所分配存储区域的第一个字节的地址，分配失败则返回空指针（NULL）。

+ 用`void *realloc(void *p, unsigend int size);`重新分配动态存储区

    在已用`malloc`或`calloc`函数分配了动态空间后想改变其大小，可用`realloc`函数重新分配，将`p`指向的动态空间大小改编为`size`，改变失败则返回空指针（NULL）。

+ 用`free(void *p);`释放动态存储区

    释放指针`p`所指向的动态空间，无返回值。

以上函数的声明在`stdlib.h`头文件中，结果是获得动态存储区的起始地址。`void`指针类型为“指向空类型”，在赋值时应注意**类型转换**。要注意的是在分配到存储区后，得到的是该区域第一个字节的地址，要使用该区域就必须使用指针。案例如下

### 2.5 内存中的栈和堆

1. 栈
2. 堆

### 2.6 建立数据类型

1. 结构体
2. 共用体
3. 枚举类型

## DataStructure & Algorithm

> 数据结构包括**逻辑结构（抽象关系）**、**存储结构**和**数据运算**，对数据类型进行抽象，**抽象数据类型**（Abstract Data Type, ADT）包括三部分：数据对象、数据关系和基本操作。

### 3.1 算法

**算法**是为了解决问题而规定的一个有限长的操作序列。一个算法必须满足以下五个特性

+ **有穷性**：有穷步骤
+ **确定性**：每种情况都有确定的结果
+ **可行性**：每一步骤可行
+ **输入**：有零个或多个输入
+ **输出**：有一个或多个输出

算法优劣的评价标准

+ 正确性：在合理的数据输入下，能在有限的运行时间内得到正确结果
+ 可读性：便于理解
+ 健壮性：当输入数据非法时，能做出正确反应
+ 高效性：包括时间和空间两方面，执行效率高和占用存储容量合理

一个程序的运行时间，依赖于算法的好坏和问题的输入规模。算法效率的度量方法主要有两类，事后统计法和事前分析估算法，通常采用**事前分析估算法**。

一条语句的重复执行次数称作**语句频度**（Frequency Count）。案例如下

```c
for(int i = 1; i <= n; i++)						// 频度为n+1
{
    for(int j = 1; j <= n; j++)					// 频度为n*(n+1)
    {
        c[i][j] = 0;						  // 频度为n^2
        for(int k = 1; k <= n; k++)				// 频度为n^2*(n+1)
            c[i][j] = c[i][j] + a[i][k] * b[k][j];	// 频度为n^3
    }
}
```

该算法中所有语句频度之和$T(n)$是结束$n$的函数，用$f(n)$表示，也就是算法的执行时间与$f(n)$成正比。

1. 算法的时间复杂度定义

    用"O"表示数量级，则上述算法可记作$T(n) = O(f(n))=O(n^3)$，表示随问题规模$n$的增大，算法执行时间的增长率和$f(n)$的增长率相同，称作算法的**渐近时间复杂度**，简称**时间复杂度**。

2. 算法的空间复杂度定义

    空间复杂度$S(n)$定义为该算法所消耗的存储空间，记作$S(n)=O(g(n))$，一般指所占用临时的工作单元数有关。

算法的时间复杂度和空间复杂度是相互影响的，通常假设运算空间充足，以时间复杂度作为算法优劣的衡量标准。

### 3.2 线性表

由有限个数据特性相同的元素构成的序列称为**线性表**，一般表示为$L = (a_1,a_2,...,a_n)$。对于非空的线性表或线性结构，有以下特点

+ 存在唯一一个“第一个”数据元素$a_1$，表头元素
+ 存在唯一一个“最后一个”数据元素$a_n$，表尾元素
+ 出第一个外，结构中的每个元素均只有一个前驱
+ 除最后一个外，结构中的每个元素均只有一个后继

![image-20250225205124061](https://cdn.jsdelivr.net/gh/Zhang-TNT/markdown-imgs@main/imgs/image-20250225205124061.png)

对线性表进行数据类型抽象：

```c
ADT List{
    数据对象：D = {ai|ai belong to ElemSet}
    数据关系：R = {<ai-1, ai>|ai-1}
    基本操作：
        InitList(&L)：初始化，构造一个空的线性表
        LengthList(L)：求表长，返回线性表L的长度
        LocateElem(L, e)：按值查找，在L中查找值为e的元素
        GetElem(L, i)：按位查找，在L中查找第i位的元素
 	    ListInsert(&L, i, e)：插入操作，在i位插入元素e
 	    ListDelete(&L, i, &e)：删除操作，e返回删除元素的值
 	    PrintList(L)：输出操作，顺序打印表L元素
 	    EmptyList(L)：判空操作
 	    DestroyList(&L)：销毁操作，销毁线性表并释放L的内存空间
 	    ClearList(&L)：清空操作
}
```

#### 3.2.1 线性表的顺序表示和实现

线性表的顺序表示是**用一段地址连续的存储单元**依次存储线性表的数据元素（顺序表索引从1开始），这种表示称作线性表的顺序存储结构或顺序映像，逻辑位序和物理位序均相差1，称这种存储结构的线性表为**顺序表**。示意图如下

![image-20250225205636641](https://cdn.jsdelivr.net/gh/Zhang-TNT/markdown-imgs@main/imgs/image-20250225205636641.png)

线性表的每个数据元素的类型都相同，即可用C语言中的一维数组来实现顺序存储结构，有两种方式

```c
// 静态分配
#define MAXSIZE 100
typedef int ElemType;
typedef struct _SqList_static	// 顺序表存储结构
{
    ElemType elem[MAXSIZE];
    int length;
}SqList_static;
// 动态分配，主要用于有指针操作的语言
#define MAXSIZE 100
typedef int ElemType;
typedef struct _SqList_dynamic
{
    ElemType *elem;
    int length;
}SqList_dynamic;
SqList_dynamic L;
L.elem = (ElemType *)malloc(sizeof(ElemType) * MAXSIZE);
```

假设线性表中每个元素占用$l$个存储单元，那么线性表中第$i+1$个元素的存储位置$LOC(a_{i+1})$和第$i$个元素的存储位置$LOC(a_i)$之间满足关系$LOC(a_{i+1})=LOC(a_i)+l$，一般来说线性表的第$i$个元素$a_i$的存储位置为$LOC(a_i)=LOC(a_1)+(i-1)l$，其中$LOC(a_1)$是线性表的**起始位置**或**基地址**。顺序表内相邻元素有相邻的存储位置，**物理位置相邻**，顺序存储结构是一种随机存取的存储结构。

1. 初始化

    构造一个空的顺序表：为L动态分配一个预定义大小的数组空间，使`elem`指向这段空间的基地址；将表的当前长度设为0。

    + 为顺序表$L$分配数组空间（静态和动态），使数据$elem$指向该段空间的基地址
    + 将表的当前长度设为0

    静态分配适合于没有指针操作的语言，实现代码如下

    ```c
    SqList_static sqlist1;	// 顺序表
    sqlist1.length = 0;		// 初始化长度
    sqlist1.elem[0] = 1;
    sqlist1.elem[1] = 2;
    sqlist1.elem[2] = 3;
    sqlist1.elem[3] = 4;
    sqlist1.length = 4;		// 存储玩数据
    ```

    动态分配适合有指针操作的语言，实现代码如下

    ```c
    Status SqList_dynamic_Init(SqList_dynamic *L)
    {
        L->elem = (ElemType *)malloc(sizeof(ElemType) * SQLIST_MAXSIZE);
        if (L->elem == NULL)
            return STATUS_ERROR;
        L->length = 0;
        return STATUS_OK;
    }
    ```

    

2. 取值

    取值操作是根据指定位置序号$i$，获取顺序表中的第$i$个数据元素的值，将其存在参数$e$中，并返回`STATUS_OK`；位置序号不合理，则返回`STATUS_INFEASIBLE`。

    + 判断指定位置$i$是否合法，非法则返回`STATUS_INFEASIBLE`
    + 将第$i$个位置数据元素值`L.elem[i-1]`赋给参数`e`

    静态分配实现代码如下

    ```c
    int SqList_static_GetElem(SqList_static L, int i)
    {
        if (i < 1 || i > L.length)
            return STATUS_ERROR;
        int e = L.elem[i - 1];
        return e;
    }
    ```

    动态分配实现代码如下

    ```c
    Status SqList_dynamic_GetElem(SqList_dynamic L, int i, ElemType *e)
    {
        if (i < 1 || i > L.length)
            return STATUS_ERROR;
        *e = L.elem[i - 1];
        return STATUS_OK;
    }
    ```

    

3. 查找

    查找操作是根据指定的元素值$e$，查找顺序表中第1个与$e$相等的元素，查找成功则返回位置序号；查找失败则返回0。

    + 从第一个元素起，依次比较`L.elem[i]`和`e`，相匹配则返回序号`i+1`
    + 查找失败则返回0

    静态分配实现代码如下

    ```c
    int SqList_static_LocateElem(SqList_static L, ElemType e)
    {
        for (int i = 0; i < L.length; i++)
        {
            if (L.elem[i] == e)
                return i + 1;
        }
        return 0;
    }
    ```

    动态分配实现代码如下

    ```c
    int SqList_dynamic_LocateElem(SqList_dynamic L, ElemType e)
    {
        for (int i = 0; i < L.length; i++)
        {
            if (L.elem[i] == e)
                return i + 1;
        }
        return 0;
    }
    ```

    

4. 插入

    插入操作是在表的$i$个位置插入一个新的数据元素$e$，使长度为$n$的线性表变为长度为$n+1$的线性表，数据元素$a_i$及其后续数据元素均向后移动一位，在算法上需要从最后一个元素即第$n$个元素开始依次向后移动一个位置，直至第$i$个元素，共移动$(n-i+1)$个数据元素。

    + 判断插入位置$i$是否合法，非法则返回`STATUS_INFEASIBLE`
    + 判断顺序表存储空间是否充足，不够则返回`STATUS_OVERFLOW`
    + 将第$n$个至第$i$个位置的元素依次向后移动一位，空出第$i$个位置
    + 将要插入的元素$e$放入第$i$个位置
    + 表长加1

    静态分配实现代码如下

    ```c
    Status SqList_static_Insert(SqList_static *L, int i, ElemType e)
    {
        if (i < 1 || i > L->length + 1)
            return STATUS_ERROR;
        if (L->length == SQLIST_MAXSIZE)
            return STATUS_ERROR;
        for (int j = L->length - 1; j >= i - 1; j--)
        {
            L->elem[j + 1] = L->elem[j];
        }
        L->elem[i - 1] = e;
        L->length++;
        return STATUS_OK;
    }
    ```

    动态分配实现代码如下

    ```c
    Status SqList_dynamic_Insert(SqList_dynamic *L, int i, ElemType e)
    {
        if (i < 1 || i > L->length + 1)
            return STATUS_ERROR;
        if (L->length == SQLIST_MAXSIZE)
            return STATUS_ERROR;
        for (int j = L->length - 1; j >= i - 1; j--)
        {
            L->elem[j + 1] = L->elem[j];
        }
        L->elem[i - 1] = e;
        L->length++;
        return STATUS_OK;
    }
    ```

    顺序表在进行数据元素的插入时，时间主要耗费在元素的移动上，移动元素的个数取决于插入元素的位置。

5. 删除

    删除操作是将表中的第$i$个元素删除，将长度为$n$的线性表变为长度为$n-1$的线性表，数据元素$a_i$其后续数据元素均向前移动一位，在算法上需要从第$i+1$个元素开始依次向前移动一个位置，直至第$n$个元素，共移动$(n-i)$个元素。

    + 判断删除位置$i$是否合法，非法则返回`STATUS_INFEASIBLE`
    + 将第$i+1$个至第$n$个位置的元素依次向前移动一个位置
    + 表长减1

    静态分配实现代码如下

    ```c
    Status SqList_static_Delete(SqList_static *L, int i)
    {
        if (i < 1 || i > L->length)
            return STATUS_ERROR;
        for (int j = i - 1; j < L->length - 1; j++)
        {
            L->elem[j] = L->elem[j + 1];
        }
        L->length--;
        return STATUS_OK;
    }
    ```

    动态分配实现代码如下

    ```c
    Status SqList_dynamic_Delete(SqList_dynamic *L, int i)
    {
        if (i < 1 || i > L->length)
            return STATUS_ERROR;
        for (int j = i - 1; j < L->length - 1; j++)
        {
            L->elem[j] = L->elem[j + 1];
        }
        L->length--;
        return STATUS_OK;
    }
    ```

    

6. 打印

    打印操作是将表中的数据元素依次打印。

    + 判断表长度是否非空
    + 遍历打印数据元素

    静态分配实现代码如下

    ```c
    void SqList_static_Print(SqList_static L)
    {
        if (L.length == 0)
            printf("[]\n");
        for (int i = 0; i < L.length; i++)
        {
            printf("L.elem[%d] = %d\n", i, L.elem[i]);
        }
    }
    ```

    动态分配实现代码如下

    ```c
    void SqList_dynamic_Print(SqList_dynamic L)
    {
        if (L.length == 0)
            printf("[]\n");
        for (int i = 0; i < L.length; i++)
        {
            printf("L.elem[%d] = %d\n", i, L.elem[i]);
        }
    }
    ```

    

7. 获取表长度

    返回表长度

    静态分配实现代码如下

    ```c
    int SqList_static_Length(SqList_static L)
    {
        return L.length;
    }
    ```

    动态分配实现代码如下

    ```c
    void SqList_dynamic_Print(SqList_dynamic L)
    {
        if (L.length == 0)
            printf("[]\n");
        for (int i = 0; i < L.length; i++)
        {
            printf("L.elem[%d] = %d\n", i, L.elem[i]);
        }
    }
    ```

    

#### 3.2.2 线性表的链式表示和实现

线性表的链式表示是**用一组任意的存储单元存储线性表的数据元素**。为表示每个数据元素$a_i$，除了存储其本身的信息之外，还需要存储一个指示其后续的信息，这两部分信息组成数据元素$a_i$的存储映像，称为**结点**，每个结点包括两个域：数据域和指针域。$n$个结点链接成一个链表，即为线性表的链式存储结构。数据元素间的逻辑关系是由结点中的指针指示的，这种存储结构为非顺序映像或链式映像。

根据链表结点所含指针个数、指针指向和指针连接方式，可将链表分为单链表、循环链表、双向链表、二叉链表、十字链表、邻接表、邻接多重表等，其中单链表、循环链表、双向链表用于实现线性表的链式存储结构，其他形式多用于实现树和图等非线性结构。下图所示为线性表的单链表存储结构，**整个链表的存取必须从头指针开始进行**，头指针为链表中的第一个结点（基地址），最后一个结点指针为空。

![image-20250225221806339](https://cdn.jsdelivr.net/gh/Zhang-TNT/markdown-imgs@main/imgs/image-20250225221806339.png)

通常将链表化成使用箭头相链接的结点序列，结点之间的箭头表示指针域中的指针，只需要表示线性表中数据元素之间的逻辑顺序即可，**单链表可由头指针唯一确定**。C语言中使用“结构指针”来描述

```c
// 单链表存储结构
typedef struct _LNode
{
    int data;
    struct _LNode *next;
}LNode;
```

这里对首元结点、头结点和头指针三个概念加以说明

![image-20250226195914911](https://cdn.jsdelivr.net/gh/Zhang-TNT/markdown-imgs@main/imgs/image-20250226195914911.png)

+ 首元结点：链表中存储第一个数据元素的结点
+ 头结点：首元结点前附设的一个结点，数据域不存储信息（或存储与数据元素类型相同的附加信息），指针域指向首元结点；头结点作用：便于首元结点处理、便于空表和非空表的统一处理
+ 头指针：指向链表中第一个结点的指针，若没有头结点时指向首元结点，是链表必要元素

注：引入头结点后，头指针的指向始终为头结点，虽然会占用内存；未引入头结点，头指针的指向会发生改变。

1. 初始化

    构建一个指向头指针的指针，即一个二重指针，生成一个新结点，二重指针指向该结点（头结点），头结点指针域为NULL。

    + 生成新结点作为头结点，由头指针指向该结点
    + 头结点指针域置空

    带头节点代码实现如下

    ```c
    // 初始化参数必须是指针，即指向头指针的指针
    Status LinkList_Init(LinkList *L)
    {
        *L = (LNode *)malloc(sizeof(LNode));	// 头指针指向头节点
        if (*L == NULL)
            return STATUS_ERROR;
        (*L)->next = NULL;	// 头节点指针域为NULL
        return STATUS_OK;
    }
    ```

    不带头节点代码实现如下

    ```c
    ```

    

2. 取值

    取值操作只能从链表的首元结点出发，顺着链域`next`逐个结点向下访问。

    + 用指针`p`指向首元结点，用`j`做计数器
    + 从首元结点开始依次顺着链域`next`向下访问，只要当前结点指针`p`不为空，且没有到达序号`i`的结点，循环执行：`p`指向下一个结点，计数器`j`加1
    + 退出循环时，如果指针`p`为空或`j`大于`i`时，说明指定的序号`i`不合法；否则取值成功，有`j=i`，`p`所指的结点即为要找的`i`号数据元素，用参数`e`保存数据

    带头结点代码实现如下

    ```c
    Status LinkList_GetElem(LinkList L, int i, ElemType *e)
    {
        LNode *pTemp = L->next;	// 指向首元结点
        int j = 1;
        while (pTemp != NULL && j < i)
        {
            pTemp = pTemp->next;
            j++;
        }
        if (pTemp == NULL || j > i)
            return STATUS_ERROR;
        *e = pTemp->data;
        return STATUS_OK;
    }
    ```

    不带头结点代码实现如下

    ```c
    ```

    

3. 查找

    查找操作是从链表首元结点出发，依次将结点值与给定值$e$进行比较，返回目标结点地址。

    + 用指针指向首元结点
    + 从首元结点出发顺着链域向下查找，当前结点$p$指针域不为空且数据域不等于给定值$e$执行循环操作：$p$指向下一个结点
    + 查找成功则返回$p$，失败则返回`STATUS_ERROR`

    带头结点代码实现如下

    ```c
    int LinkList_LocateElem(LinkList L, ElemType e)
    {
        LNode *pTemp = L->next;
        int i = 1;
        while (pTemp != NULL)
        {
            if (pTemp->data == e)
                return i;
            pTemp = pTemp->next;
            i++;
        }
        return 0;
    }
    ```

    不带头结点代码实现如下

    ```c
    ```

    

4. 插入

    插入操作是在表的第$i$个位置插入一个值为$e$的新结点$s$，插入到$a_{i-1}$到$a_i$之间。

    + 查找结点$a_{i-1}$
    + 创建新结点$s$，数据域为$e$，指针域为$a_i$
    + 将结点$a_{i-1}$的指针域更改为结点$s$

    带头结点代码实现如下

    ```c
    Status LinkList_Insert(LinkList *L, int i, ElemType e)
    {
        if (i < 1)
            return STATUS_ERROR;
    
        LNode *pTemp = (*L); // pTemp指向头结点
        int j = 0;
        while (pTemp != NULL && j < i - 1)
        {
            pTemp = pTemp->next;
            j++;
        }
        if (pTemp == NULL || j > i - 1)
            return STATUS_ERROR;
        LNode *pNode = (LNode *)malloc(sizeof(LNode));
        if (pNode == NULL)
            return STATUS_ERROR;
        pNode->data = e;
        pNode->next = pTemp->next;
        pTemp->next = pNode;
        return STATUS_OK;
    }
    ```

    不带头结点代码实现如下

    ```c
    ```

    

5. 删除

    删除操作是将链表中的第$i$个位置的结点$p$删除，首先找到其前驱结点$o$，然后修改$o$的指针域即可。

    + 查找结点$a_{i-1}$，由指针$p$指向该结点
    + 临时保存结点$a_i$的地址在$q$中
    + 将结点$*p$的指针域指向$a_i$的后继结点
    + 释放结点$a_i$的空间

    带头结点代码实现如下

    ```c
    Status LinkList_Delete(LinkList L, int i)
    {
        LNode *pTemp = L->next; // pTemp指向首元结点
        int j = 1;
        while (pTemp != NULL && j < i - 1)
        {
            pTemp = pTemp->next;
            j++;
        }
        if (pTemp == NULL || j > i - 1)
            return STATUS_ERROR;
        LNode *pNode = pTemp->next;
        if (pNode == NULL)
            return STATUS_ERROR;
        pTemp->next = pNode->next;
        free(pNode);
        return STATUS_OK;
    }
    ```

    不带头结点代码实现如下

    ```c
    ```

    

6. 打印

    打印链表数据域操作是从链表头指针$phead$出发，顺着链域向下遍历，在链域不为`NULL`条件下打印数据域。

    + 新建结点指向首元结点
    + 顺着首元结点向下检索直到尾节点

    带头结点代码实现如下

    ```c
    void LinkList_Print(LinkList L)
    {
        LNode *pTemp = L->next; // pTemp指向首元结点
        int i = 0;
        if (pTemp == NULL)
            printf("[]\n");
        else
        {
            while (pTemp != NULL)
            {
                printf("L.elem[%d] = %d\n", i + 1, pTemp->data);
                pTemp = pTemp->next;
                i++;
            }
        }
        printf("\n");
    }
    ```

    不带头结点代码实现如下

    ```c
    ```

    

7. 获取长度

    求链表长度操作是从链表的头指针$phead$出发，设置计数器，顺着链域向下寻找，在链域不为`NULL`前提下进行计数，直至遇到`NULL`计数结束，即为链表长度。

    + 新建结点指向首元结点
    + 新建计数器从零开始计数
    + 顺着首元结点向下检索，结点指针域不为NULL则计数器加1，直到尾节点

    带头结点代码实现如下

    ```c
    int LinkList_Length(LinkList L)
    {
        int len = 0;
        LNode *pTemp = L->next; // pTemp指向首元结点
        while (pTemp != NULL)
        {
            len++;
            pTemp = pTemp->next;
        }
        return len;
    }
    ```

    不带头结点代码实现如下

    ```c
    ```

#### 3.2.3 顺序表和链表比较

+ 空间性能

    顺序表必须预先分配空间，已造成存储空间浪费或空间溢出；链表不需预先分配空间，元素个数没有限制。

    由于链表每个结点还要额外设置指针域，从存储密度上讲是不经济的。

+ 时间性能

    顺序表是一种随机存取结构，存取元素时间复杂度为$O(1)$；链表存取元素必须检索全链表，存取元素时间复杂度为$O(n)$。

#### 3.2.4 其他链表

对于单链表，结点中的指针域只存储了向后的指针，不能满足一些复杂问题，因此提出以下链表。

+ 循环链表

    将单链表中终端尾节点指针由NULL改为指向头节点，就使得整个单链表形成一个换，这种头尾相接的单链表称为**单循环链表**。示意图如下

    ![image-20250226212555556](https://cdn.jsdelivr.net/gh/Zhang-TNT/markdown-imgs@main/imgs/image-20250226212555556.png)

+ 双向链表

    双向链表就是在单链表的每个结点中，在设置一个指向其前驱结点的指针域，使得链表可以双向检索。

    ![image-20250226212848349](https://cdn.jsdelivr.net/gh/Zhang-TNT/markdown-imgs@main/imgs/image-20250226212848349.png)

#### 3.2.5 线性表的应用

线性表是其他数据结构的基础，因此应用非常广泛。

### 3.3 栈与队列

#### 3.3.1 栈

1. 定义

    栈（stack）是限定**仅在表尾进行插入或删除操作的线性表**。表尾称为**栈顶**，表头称为**栈底**；栈是自动管理的内存区域，系统进行自动分配和释放内存，采取先进后出**（FILO）**的原则，连续存储数据。栈的示意图如下所示

    ![image-20250226214033219](https://cdn.jsdelivr.net/gh/Zhang-TNT/markdown-imgs@main/imgs/image-20250226214033219.png)

    栈对线性表的插入和删除位置进行了限制，**但并没有对元素进出的时间进行限制**，事先进入的元素也可最先出栈。

2. 栈的抽象数据类型

    对栈来说，将其插入和删除操作，改名为`push`和`pop`，即压栈和弹栈。基本操作还有栈的初始化、栈的长度、获取栈顶元素等，栈的抽象数据类型如下

    ```c
    ADT Stack{
            数据对象：D = {ai|ai belong to ElemSet}
        	数据关系：R = {<ai-1, ai>|ai-1, ai belong to D}
        	基本操作：
                InitStack(&S)：初始化
                DestroyStack(&S)：销毁
                ClearStack(&S)：清空
                StackEmpty(S)：是否空栈
                StackLength(S)：栈长度
                GetTop(S)：返回栈顶元素
                Push(&S, e)：将e压入栈
                Pop(&S, &e)：删除栈顶元素，用e返回
                StackTraverse(S)：遍历栈
    }ADT Stack

3. 表示和实现

    既然栈是线性表的特例，那么栈也有**顺序栈**、**链式栈**两种存储表示方式。

    + 顺序栈

        顺序栈可表示如下

        ```c
        /* sequence Stack structure static */
        typedef struct _SqStack
        {
            ElemType elem[SQLIST_MAXSIZE];
            int top;
        } SqStack;
        
        /* sequence Stack structure dynamic */
        typedef struct _SqStack_dynamic
        {
            ElemType *elem;
            int top;
        } SqStack_dynamic;
        
        /* sharing sequence Stack structure */
        typedef struct _SqStack_shared
        {// 共享栈使用同一段内存空间，一个栈的栈底为数组始端“0”处，另一个栈的栈底为数组末端“n-1”处，两栈向中间靠拢。栈1为空时，top1=-1；栈2为空时，top2=n。两者栈顶相差1时，为栈满。
            ElemType elem[STACK_MAXSIZE];
            int top1;
            int top2;
        } _SqStack_shared;
        ```

        + 初始化

            顺序栈的初始化操作就是为顺序栈分配一块内存空间，将栈置为空。

            ```c
            void Stack_Init(SqStack *S)
            {
                S->top = -1; // 初始化栈为空
            }
            ```

            

        + 清空栈

            顺序栈的清空操作就是将栈置为空，丢弃所存储的数据。

            ```c
            void Stack_Clear(SqStack *S)
            {
                S->top = -1; // 清空栈
            }
            ```

            

        + 压栈

            顺序栈的压栈操作就是在栈顶插入一个新的元素

            ```c
            Status Stack_Push(SqStack *S, ElemType e)
            {
                if (S->top == STACK_MAXSIZE - 1)
                    return STATUS_ERROR;
                S->top++;            // 栈顶指针向上移
                S->elem[S->top] = e; // 将元素插入栈顶
                // S->elem[++S->top] = e;
                return STATUS_OK;
            }
            ```

            

        + 弹栈

            顺序栈的弹栈操作就是删除栈顶元素

            ```c
            Status Stack_Pop(SqStack *S, ElemType *e)
            {
                if (S->top == -1)
                    return STATUS_ERROR;
                *e = S->elem[S->top];
                S->top--; // 栈顶指针向下移
                return STATUS_OK;
            }
            ```

            

        + 获取栈顶元素

            顺序栈的获取栈顶元素操作

            ```c
            Status Stack_GetTop(SqStack S, ElemType *e)
            {
                if (S.top == -1)
                    return STATUS_ERROR;
                *e = S.elem[S.top];
                return STATUS_OK;
            }
            ```

            

        + 栈长度

            顺序栈的长度

            ```c
            int Stack_Length(SqStack S)
            {
                return S.top + 1;
            }
            ```

            

        + 栈遍历打印

            顺序栈的遍历打印

            ```c
            void Stack_Print(SqStack S)
            {
                for (int i = S.top; i > -1; i--)
                {
                    printf("Stack.elem[%d] = %d \n", i, S.elem[i]);
                }
                printf("\n");
            }
            ```

            

    + 链式栈

        链式栈可表示如下

#### 3.3.2 栈的应用

1. 栈

    在软件应用中，如浏览器网页的后退键，能返回之前所浏览的网页；还有编辑软件这撤销功能，可撤销上次操作。这些功能的实现都是通过**栈**这种数据结构实现。

2. 



#### 3.3.3 队列

1. 定义

    队列（queue）是一种先进先出（FIFO）的线性表，**限定仅在表的一端进行插入元素，而在另一端删除元素**，允许插入的一端称为**队尾**，允许删除的一端称为**队头**。队列的示意图如下所示

2. 队列的抽象数据类型

3. 表示和实现

#### 3.3.4 队列的应用

