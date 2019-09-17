### 1. C++ Output and Language Basics 

```C++
#include <iostream>
using std::cout;

int main() {
    cout << "Hello!" << "\n";   
}
```
#### #include

* The #include is a preprocessor command which is executed before the code is compiled. 

    #include 语句是一条预处理命令，该语句在编译之前被执行。

* It searches for the iostream header file and pastes its contents into the program. iostream contains the declarations for the input/output stream objects.

    #include 语句搜索头文件iostream并将该头文件的内容加入待编写的程序中。iostream中包含输入/输出流对象的声明。

#### using std::cout

- Namespaces are a way in C++ to group identifiers (names) together. They provide context for identifiers to avoid naming collisions. The std namespace is the namespace used for the standard library. 

    命名空间是为了避免命名冲突。std用于标准库的命名空间。

- The using command adds std::cout to the global scope of the program. This way you can use cout in your code instead of having to write std::cout.

    在程序的全局范围内加上 std::cout 语句后，可以在代码中直接使用cout函数，避免写 std::cout。

- cout is an output stream you will use to send output to the notebook or to a terminal, if you are using one.

    cout 是一个输出流，可以向终端中输出信息。

- Note that the second two lines in the example end with a semicolon ;. Coding statements end with a semicolon in C++. The #include statement is a preprocessor command, so it doesn't need one.

#### cout << "Hello!" << "\n"; 

- In this line, the code is using cout to send output to the notebook. The << operator is the stream insertion operator, and it writes what's on the right side of the operator to the left side. So in this case, "Message here" is written to the output stream cout. 

    <<运算符是流插入运算符，它将运算符右侧的内容写入左侧。



### 2. Vector Containers

#### 1D Vectors 

​	Vectors are a sequence of elements of a single type, and have useful methods for getting the size,testing if the vector is empty, and adding elements to the vector.

​	Vectors 是相同类型变量的一个序列，有获取序列大小，判断是否为空和加入新元素的方法。

#### 2D Vectors 

​	Unfortunately, there isn't a built-in way to print vectors in C++ using cout. You will learn how to access vector elements and you will write your own function to print vectors later. For now, you can see how vectors are created and stored. Below, you can see how to nest vectors to create 2D containers.

​	对于二维Vector，C++ 中并没有内置输出的方法。

```c++
#include <iostream>
#include <vector>
using std::cout;
using std::vector;


int main(){

    //1d
    vector<int> v1{0,1,2};
    vector<int> v2 = {3,4,5};
    vector<int> v3;
    v3 = {6,7,8};
    cout << "1d initial ok"<<"\n";
    //cout << v1[2] << "\n";
    cout << v2[0] << "\n";
    cout << v3[1] << "\n";


    //2d
    vector<vector<int>> v2d {{1,2},{7,8}};
    cout << "2d initial ok"<<"\n";
    cout << v2d[1][1] << "\n";

}
```



### 3.  C++ Comments

You may have noticed comments in some of the code up until this point. C++ provides two kinds of comments:

```C++
// You can use two forward slashes for single line comments.

/*
For longer comments, you can enclose the text with an opening
slash-star and closing star-slash.
*/ 
```



### 4. Using Auto

In your previous code, the type for each variable was explicitly declared. In general, this is not necessary, and the compiler can determine the type based on the value being assigned.

```c++
#include <iostream>
#include <vector>
using std::vector;
using std::cout;

int main() {
    auto i = 5;
    auto v_6 = {1, 2, 3,7,8,9};
    cout << "Variables declared and initialized without explicitly stating type!" << "\n";

    for (auto i :v_6){
        cout << i << " ";
    }
    cout << "\n";
}
```

It is helpful to manually declare the type of a variable if you want the variable type to be clear for reader of your code, or if you want to be explicit about the number precision being used; C++ has several number types with different levels of precision, and this precision might not be clear from the value being assigned.

如果为了增加代码的易读性或者已经明确要使用数字的精度，手动声明便利可能会更好。C++ 不同的变量类型有着不同的精度，从分配的值中无法获取具体精度如何。