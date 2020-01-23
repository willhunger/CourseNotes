1. const 和 constexpr 

    * 基本含义 / 语法 

        const和constexpr都可以来修饰对象和函数。

        1. 修饰对象的时候两者之间最基本的区别是：
            * const修饰一个对象表示它是常量。这暗示对象一经初始化就不会再变动了，并且允许编译器使用这个特点优化程序。这也防止程序员修改了本不应该修改的对象。
            * constexpr是修饰一个常量表达式。但请注意constexpr不是修饰常量表达式的唯一途径。
        2. 修饰函数的时候两者之间最基本的区别是：
            * const只能用于非静态成员的函数而不是所有函数。它保证成员函数不修改任何非静态数据。
            * constexpr可以用于含参和无参函数。constexpr函数适用于常量表达式，只有在下面的情况下编译器才会接受constexpr函数： 1.函数体必须足够简单，除了typedef和静态元素，只允许有return语句。如构造函数只能有初始化列表，typedef和静态元素 (实际上在C++14标准中已经允许定义语句存在于constexpr函数体内了) 2.参数和返回值必须是字面值类型

    * 常量表达式 

        常量表达式的概念如下：

        * 必须是可以在编译阶段被识别的。比如模版的参数／数组的大小。

        * ```C++
            template <int N>
            class fixed_size_list
            { /*...*/ };
            
            fixed_size_list<X> mylist;     // <-- X必须是字面值类型
            
            int numbers[X];   // <-- X必须是字面值类型
            ```

        但是要注意以下两点：

        1. 用constexpr修饰某物并不保证它一定在编译时被计算，也可以在运行时被计算。

        2. 不用constexpr也可能是一个常量表达式，如 

            ```C++
            int main()
            {
            const int N = 3;
            int num[N] = {1,2,3,};//N是一个常量表达式}
            //N在声明时初始化，满足常量表达式的标准，虽然没用constexpr
            ```

    * 所以到底什么时候用constexpr?

        * 像上面的N，虽然没有用 constexpr 仍然是一个常量表达式。事实上，const本身和它的枚举类型若在声明时初始化那么就是一个常量表达式。

        * 在函数中若有常量表达式那么必须用constexpr，仅仅满足常量表达式的条件是不够的，如

            ```C++
            template <int N>
            class list
            { };
            
            constexpr int sqr1(int arg)
            { return arg*arg; }
            
            int sqr2(int arg)
            { return arg*arg; }
            
            int main()
            {
            const int X = 2;
            
            list<sqr1(X)> mylist1;//可以，因为sqr1时constexpr函数
            list<sqr2(X)> mylist2;//不可以，因为sqr2不是constexpr函数
            return 0;}
            ```

            

    * 什么时候该同时使用两者？ 

        * 在修饰变量的时候

            修饰变量时没有必要同时使用const和constexpr 因为constexpr包含了 const的含义。

            ```C++
            constexpr const int N = 5;
            constexpr int N = 5;
            //两行的意思完全相同
            ```

        * 然而注意有一些情况const和constexpr在修饰不同的东西，比如

            ```C++
            static constexpr int N = 3;
            int main()
            {
                constexpr const int *NP = &N;
                return 0;
            }
            ```

            在这里constexpr和const都必须要有。constexpr表示NP指针本身是常量表达式，而const表示指向的值是一个常量。去掉const之后无法编译，因为不能用正常指针指向常量。

        * 在修饰成员函数的时候

            在C++11中，对成员函数而言constexpr同样包含const的含义。然而在C++14中可能已经改变了。如

            ```C++
            constexpr void f();
            ```

            以后可能必须写成

            ```C++
            constexpr void f() const;
            ```

            虽然目前写成const仍然有效，但最好使用constexpr来防止以后修改大量代码的可能性。

            

2. C++ reference vs pointer

    [Pointers, References and Dynamic Memory Allocation](https://www.ntu.edu.sg/home/ehchua/programming/cpp/cp4_PointerReference.html) 

    

3. A* Search 

4. Reference 

    [浅谈 C++ 中的 const 和 constexpr](https://zhuanlan.zhihu.com/p/20206577) 

    [Difference between constexpr and const](https://stackoverflow.com/questions/14116003/difference-between-constexpr-and-const)

    [C++ const 和 constexpr 的区别？](https://www.zhihu.com/question/35614219) 

    