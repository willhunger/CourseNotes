#### Write Your First C++ Program
C++ is a `compiled language`; there is `a separate program - the compiler` - that converts your code to an `executable program` that the computer can run. This means that running a new C++ program is normally a two step process:    
C++是一种编译语言，有一个单独的程序编译器，将您的代码转换为计算机可以运行的可执行程序。这意味着运行C++需要两个步骤：

1. `Compile` your code with a compiler.
To compile, use the following command: `g++ main.cpp`
使用编译器编译你的代码
2. `Run the executable file` that the compiler outputs.
To run, use: `./a.out`
运行编译器输出的可执行文件

main() should `return an integer` (an int in C++), which indicates if the program exited successfully. This is specified in code by writing the return type, followed by the main function name, followed by empty arguments:    
main()函数应该返回一个整数，它表示程序是否成功退出，这是在代码中通过编写返回类型，后跟main函数名称，以及空参数来指定的
```
int main()
```
The body of the main(), which comes after the main function name and arguments, is enclosed in curly brackets: `{ and }`.    
main()的主体位于主函数名和参数之后，用大括号括起来

#### C++ Output and Language Basics
```c++
#include <iostream>
using std::cout;

int main() {
    cout << "Hello!" << "\n";   
}
```
/* Review

 #include <iostream>

- The `#include is a preprocessor command` which is executed before the code is compiled. It `searches for` the iostream header file and `pastes its contents into the program`. iostream contains the declarations for the input/output stream objects   
'#include一个预处理命令，它在编译代码之前执行，它搜索iostream头文件并将其内容粘贴到程序中，iostream包含输入/输出流对象的声明。

using std::cout;

- Namespaces are a way in C++ to group identifiers (names) together. They provide context for identifiers to `avoid naming collisions`. The std namespace is the namespace used for `the standard library`.    
  命名空间是C ++中用于将标识符（名称）组合在一起的一种方式。 它们为标识符提供了“避免命名冲突”的上下文。 std命名空间是用于“标准库”的命名空间。
  
- `The using command` adds std::cout to `the global scope of the program`. This way you can use cout in your code instead of having to write std::cout.    
   using命令将std :: cout添加到程序的全局范围。 这样你就可以在代码中使用cout而不必编写std :: cout。

- `cout is an output stream` you will use to send output to the notebook or to a `terminal`, if you are using one.    
  cout是一个输出流用于将输出发送到笔记本或“终端”，如果你使用的话。
  
- Note that the second two lines in the example `end with a semicolon ;`.     
  请注意，示例中的后两行以分号结束;
  
- `Coding statements` end with a semicolon in C++. `The #include statement` is a preprocessor command, so it doesn't need one.    
  Coding语句以C ++中的分号结尾。 #include语句是一个预处理器命令，所以它不需要分好结尾。

cout << "Hello!" << "\n";

- In this line, the code is using cout to send output to the notebook. The << operator is `the stream insertion operator`, and it writes what's on `the right side of` the operator `to the left side`. So in this case, "Message here" is written to the output stream cout.    
  在这一行中，代码使用cout将输出发送到笔记本。 <<运算符是流插入运算符，它将“运算符”的右侧的内容写入左侧。 所以在这种情况下，“Message here”被写入输出流cout。
*/

#### C++ Storing Primitive Types(原始的类型)
Unlike some other languages, however, in `C++ each variable has a fixed type`. When a new variable is "declared", or introduced in a program, the program author must (usually) specify the variable type in the declaration.    
C++每一个变量都必须有一个固定的类型
```c++
#include <iostream>
#include <string>
using std::cout;

int main() {
    // Declaring and initializing an int variable.
    int a = 9;
    
    // Declaring a string variable without initializing right away.
    std::string b;
    
    // Initializing the string b.
    b = "Here is a string";
    
    cout << a << "\n";
    cout << b << "\n";
}
```
```c++
#include <iostream>
#include <vector>

using std::cout;
using std::vector;

int main(){
    // TODO: Declare a "board" variable here, and store
    // the data provided above.
    
    vector<vector<int>>  board {{0, 1, 0, 0, 0, 0},
                                {0, 1, 0, 0, 0, 0},
                                {0, 1, 0, 0, 0, 0},
                                {0, 1, 0, 0, 0, 0},
                                {0, 0, 0, 0, 1, 0}};

}

```
#### C++ Storing Vector.(a Data Structure)
/* Vector Containers

- 1D Vectors

C++ also has several `container types` that _can be used for storing data_.
We will start with `vectors`, as these will be used throughout this lesson,
but we will also introduce other container types as needed.    
 C ++还有几个`容器类型`_可用于存储data_。
我们将从`vectors`开始，因为这些将在本课程中使用，
但我们还会根据需要介绍其他容器类型。

Vectors are `a sequence of elements of a single type`, and have `useful method`s for getting the size,testing if the vector is empty, and adding elements to the vector.    
向量是“单个类型的元素序列”，并且具有用于获取大小的“有用方法”，测试向量是否为空，以及向向量添加元素。

- 2D Vectors

Unfortunately, there isn't a built-in way to print vectors in C++ using cout. You will learn how to `access vector elements` and you will write your own function to print vectors later. For now, you can see `how vectors are created and stored`. Below, you can see `how to nest vectors` to create 2D containers.    
不幸的是，没有一种使用cout在C ++中打印矢量的内置方法。 您将学习如何“访问矢量元素”，然后您将编写自己的函数以便稍后打印矢量。 现在，你可以看到`如何创建和存储向量。 下面，您可以看到“如何嵌套矢量”来创建2D容器。
*/



#### Using Auto
You have now seen how to store basic types and vectors containing those types. As you practiced declaring variables, in each case you indicated the type of the variable. It is possible for C++ to do automatic type inference, using the `auto keyword`.    
您现在已经了解了如何存储包含这些类型的基本类型和向量。 在练习声明变量时，在每种情况下都指出了变量的类型。 C ++可以使用auto关键字进行自动类型推断。

/* Using auto
In your previous code, the type for each variable was `explicitly declared`.
In general, this is not necessary, and the compiler can determine the type based on the value being assigned.
To have the type automatically determined, use the auto keyword. You can test this by executing the cell below:   
*/
/*使用auto在之前的代码中，显式声明了每个变量的类型。
通常，这不是必需的，并且编译器可以基于所分配的值来确定类型。
要自动确定类型，请使用auto关键字。 您可以通过执行以下单元格来测试：*/

/*
It is helpful to manually declare the type of a variable if you want the variable type to be `clear for reader` of your code, 
or if you want to be explicit about `the number precision` being used; 
C++ has several number types with different levels of precision, 
and this precision might not be clear from the value being assigned.
*/   
/*如果希望为代码的读者清楚变量类型，手动声明变量的类型会很有帮助，
或者如果你想明确使用的数字精度;
C ++有几种具有不同精度级别的数字类型，并且从分配的值可能不清楚这种精度。*/

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

#### Store a Grid
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
    cout << v1[2] << "\n";
    cout << v2[0] << "\n";
    cout << v3[1] << "\n";


    //2d
    vector<vector<int>> v2d {{1,2},{7,8}};
    cout << "2d initial ok"<<"\n";
    cout << v2d[1][1] << "\n";

}
```

#### Working with Vectors
You `declared and initialized `vectors in a previous notebook, but in order for the vector to be useful, you will need to be able to `retrieve` the vector elements.   
您在之前的课程中声明并初始化了向量，但为了使向量有用，您需要能够检索向量元素。
```c++
#include <iostream>
#include <vector>
using std::vector;
using std::cout;

int main() {

    //////////////////////
    //1D Vector Access
    /////////////////////
    vector<int> a = {0, 1, 2, 3, 4};
    cout << a[0];
    cout << a[1];
    cout << a[2];
    cout << "\n";
    //Getting a Vector's Length
    cout << a.size()<<"\n";

    ////////////////////////
    //2D Vector Access
    ///////////////////////
    vector<vector<int>> b = {{1, 1, 2, 3},
                             {2, 1, 2, 3},
                             {3, 1, 2, 3}};

    cout << b[2][1];
    cout << "\n";
    //Getting a Vector's Length
    cout << b.size()<<"x"<<b[0].size()<<"\n";

}
```

#### For Loops
```c++
#include <iostream>
using std::cout;

int main() {
    /* For Loop with an Index Variable */
    for (int i=0; i < 5; i++) {
        cout << i << "\n";
    }


    /* The Increment Operator */
    auto i = 1;

    // Post-increment assigns i to c and then increments i.
    auto c = i++;

    cout << "Post-increment example:" << "\n";
    cout << "The value of c is: " << c << "\n";
    cout << "The value of i is: " << i << "\n";
    cout << "\n";

    // Reset i to 1.
    i = 1;

    // Pre-increment increments i, then assigns to c.
    c = ++i;

    cout << "Pre-increment example:" << "\n";
    cout << "The value of c is: " << c << "\n";
    cout << "The value of i is: " << i << "\n";
    cout << "\n";

    // Decrement i;
    i--;
    cout << "Decrement example:" << "\n";
    cout << "The value of i is: " << i << "\n";


    /* For Loop with a Container */
    // C++ offers several ways to iterate over containers. 
    // One way is to use an index-based loop as above. 
    // Another way is using a "range-based loop", which you will see frequently in the rest of this course.
    vector<int> a {1, 2, 3, 4, 5};
    for (int i: a) {
        cout << i << "\n";
    }
}
```

#### Functions
When a function is declared and defined in a single C++ file, `the basic syntax` is as follows:
```c++
return_type FunctionName(parameter_list) {
  // Body of function here.
}
```
```c++
//AdditionFunction
#include <iostream>
using std::cout;

// Function declared and defined here.
int AdditionFunction(int i, int j) 
{
    return i + j;
}

int main() 
{
    auto d = 3;
    auto f = 7;
    cout << AdditionFunction(d, f) << "\n";
}
```
```c++
//PrintStrings
#include <iostream>
#include <string>
using std::cout;
using std::string;

// Write the PrintStrings function here.
void PrintStrings(string a, string b)
{
    cout << a << " " << b << "\n";
}


int main() 
{
    string s1 = "C++ is";
    string s2 = "super awesome.";
    
    // Uncomment the following line to call your function:
    PrintStrings(s1, s2);
}
```
```c++
//VectorAddition
#include <vector>
using std::cout;
using std::vector;

// Define a function "AdditionFunction" here.
// Instead of just two ints, this function should accept a vector<int> 
// as the argument, and it should return the sum of all the ints in the vector.

int AdditionFunction(vector<int> v) 
{
    int sum = 0;
    for (int num: v) 
    {
        sum += num;
    }

    return sum;
}

int main() 
{
    vector<int> v {1, 2, 3};
    
    // Uncomment the following line to call your function:
    cout << AdditionFunction(v) << "\n";
}
```

#### Print the Board
```c++
#include <iostream>
#include <vector>
using std::cout;
using std::vector;


// TODO: Add PrintBoard function here.
void PrintBoard(vector<vector<int>> board){
    int row = board.size();
    int col = board[0].size();

    for(int i=0; i < row; i++){
        for(int j=0; j < col; j++)
            cout << board[i][j];
        cout<<"\n";
    }
}


int main(){
    vector<vector<int>> board{{0, 1, 0, 0, 0, 0},
                              {0, 1, 0, 0, 0, 0},
                              {0, 1, 0, 0, 0, 0},
                              {0, 1, 0, 0, 0, 0},
                              {0, 0, 0, 0, 1, 0}};

    PrintBoard(board);
}
```

#### if Statements and While Loops
/*
C++ if statements work very similarly to if statements in other languages. In C++, the boolean condition is contained in parentheses ( and ), and the body of the statement is enclosed in curly brackets { and }.   
C ++ if语句与其他语言中的if语句非常相似。 在C ++中，布尔条件包含在括号（和）中，语句的主体用大括号{和}括起来。
*/
```c++
#include <iostream>
using std::cout;

int main() {
    // Set a equal to true here.
    bool a = true;

    if (a) {
      cout << "Hooray! You made it into the if statement!" << "\n";
    }
}

```
/* Practice
In the following code cell, you will combine a while loop with an if statement to print every other number. 
Write a while loop to iterate over the integers from 1 to 10. If the integer is even, print it out.    
在下面的代码单元格中，您将结合使用while循环和if语句来打印其他所有数字。
编写一个while循环来迭代1到10之间的整数。如果整数是偶数，则将其打印出来。
Hint: you can tell if an integer is even by looking at its remainder after dividing by two.
In C++, the remainder operator is %. 
In other words, for a given int i, you have remainder = i % 2. 
If remainder equals 0, the number is even.   
提示：你可以通过在除以2之后查看其余数来判断整数是否均匀。
在C ++中，余数运算符是％。
换句话说，对于给定的int i，您有余数= i％2。
如果余数等于0，则数字是偶数
*/
```c++
#include <iostream>
using std::cout;

int main() 
{
    int i = 1;

    while (i <= 10 ) {
      if (i % 2 == 0) {
        cout << i << "\n";
      }
      i++;
    }
}
```
/*
The syntax for a while loop looks very similar to the syntax for the if statement.   
while循环的语法看起来与if语句的语法非常相似。
*/
```c++
#include <iostream>
using std::cout;

int main() 
{
    auto i = 0;

    while (i < 5) {
      cout << i << "\n";
      i++;
    }
}
```

#### Reading from a File
/*
Four steps to reading a file:
1.#include <fstream>
2.Create a std::ifstream object using the path to your file.
3.Evaluate the std::ifstream object as a bool to ensure that the stream creation did not fail.
4.Use a while loop with getline to write file lines to a string.   
阅读文件的四个步骤：  
1.#include <fstream>   
2.使用文件路径创建std :: ifstream对象。   
3.将std :: ifstream对象评估为bool，以确保流创建不会失败。   
4.使用getline循环将文件行写入字符串。   
*/

```c++
#include <iostream>
#include <string>

//add this for file
#include <fstream>


void file_open_testing(){
    //initial a fstream object
    //std::fstream my_file;
    //my_file.open(path)

    //or initial in one line
    //std::ifstream my_file(path);
    std::fstream my_file;
    my_file.open("files/1.board");

    //this instance my_file can use as boolean to check is the file exist or not
    if (my_file){
        std::cout << "we have this file" << "\n";
    }else{
        std::cout << "we DON'T have this file" << "\n";
    }
}


void reading_data_from_stream(){
    std::fstream my_file("files/1.board");
    if(my_file){
        std::cout << "The file stream has been created!" << "\n";
        std::string line;
        while (getline(my_file, line)){
            std::cout << line << "\n";
        }
    }
}

int main(){
    file_open_testing();
    reading_data_from_stream();
}
```

#### Read the Board from a File
```c++
#include <iostream>
#include <string>
#include <vector>
using std::cout;
using std::string;
using std::vector;

#include<fstream>
using std::fstream;

// TODO: Add the ReadBoardFile function here.
void ReadBoardFile(string file_path){
    fstream board_file(file_path);
    if(board_file){
        string line;
        while(getline(board_file,line)){
            cout << line << "\n";
        }
    }else{
        cout<< "no such file "<< file_path << "\n";
    }

}

// PrintBoard not used in this exercise
void PrintBoard(const vector<vector<int>> board) {
  for (int i = 0; i < board.size(); i++) {
    for (int j = 0; j < board[i].size(); j++) {
      cout << board[i][j];
    }
    cout << "\n";
  }
}

int main() {
  // TODO: Call the ReadBoardFile function here.
  string file_path = "files/1.board";
  ReadBoardFile(file_path);
  // Leave the following line commented out.
  //PrintBoard(board);
}

```

#### Processing String
Now that the board is being read into your program line by line, you will want to process each line and store the data, rather than just streaming it to `cout`. There are many ways to do this in C++, but we will focus on `istringstream` from the `<sstream>` header file.   
既然board正在逐行读入您的程序，您将需要处理每一行并存储数据，而不是仅将其流式传输到cout。 在C ++中有很多方法可以做到这一点，但我们将关注来自<sstream>头文件的istringstream。

Streaming ints from a string with istringstream   
使用istringstream从字符串流式传输int

In C++ strings can be streamed into `temporary variables`, similarly to how files can be streamed into strings. 
`Streaming a string` allows us to work with each character individually.   
在C ++中，字符串可以流式传输到“临时变量”，类似于文件如何流式传输到字符串中。Streaming a string允许我们单独处理每个字符。

One way to stream a string is to use an input string stream object istringstream from the <sstream> header.   
流式传输字符串的一种方法是使用<sstream>标头中的输入字符串流对象istringstream。

Once an istringstream object has been created, parts of the string can be streamed and stored using the "`extraction operator`": >>.
The extraction operator will read until `whitespace` is reached or until the stream fails.    
一旦创建了一个istringstream对象，就可以使用“extract operator”流式传输和存储部分字符串：>>。
提取操作符将一直读到“空格”或直到流失败。

```c++
/////////////////////////
// Read int from file string
// 1. #include<sstream>
// 2. using std::istringstream
// can read string and stop only hit space or error(end)
/////////////////////////


#include <iostream>
#include <string>
#include <sstream>

using std::cout;
using std::string;
using std::istringstream;


/*
myreader is a pointer, whith point to the contain of string.
if the current pointer READ(>>) the non-number or error or endoffile
the myreader will return error or 0 or false

every time you extract a contain, the myrerader will move right to next contain.
*/


void istringstream_test(){
    cout << __func__<< "\n";

    string a("1 2 3");

    istringstream my_stream(a);

    int n;
    my_stream >> n;
    cout << n << "\n";
}


void use_isstringstream_as_boolen_read_all(){
    cout << __func__<< "\n";

    string a("1 2 3");

    istringstream my_stream(a);

    int n;
    
    // Testing to see if the stream was successful and printing results.
    while (my_stream) {
        my_stream >> n;
        if (my_stream) {
            cout << "That stream was successful: " << n << "\n";
        }
        else {
            cout << "That stream was NOT successful!" << "\n";            
        }
    }
}

void common_way_to_use_istringstream_in_while(){
    cout << __func__<< "\n";

    istringstream myreader("1 2 3");
    int n;
    while(myreader>>n){
        cout << "read: "<< n << "\n";
    }
    cout << "The stream has failed or ended." << "\n";
}



void string_with_MIX_types_not_space(){
/*
In the stream example above, the string contained only whitespaces
and characters which could be converted to ints.

If the string has mixed types, more care is needed to process the string.
In the following example,
the type char is used, which is a type that can hold only a single ASCII character.
*/
    cout << __func__<< "\n";

    string b("1,2,3,4,6q7p8o9");

    istringstream mixstring(b);

    //need two type of tmp value
    char c;
    int n;

    /*
        !! notice that the 9 was not printed

        mixstring >> n >> c

        tried to stream an int followed by a char.
        Since there was no char after the 9, the stream
        failed and the while loop exited.
    */
    while(mixstring >> n >> c){
        cout << "read int: "<< n << ", read char: " << c << "\n";
    }
    cout << "The stream has failed or ended." << "\n";
}


int main(){
    //stream with all INT type
    istringstream_test();
    use_isstringstream_as_boolen_read_all();
    common_way_to_use_istringstream_in_while();

    //stream with MIX type
    //the INT spreated by only one char not space
    string_with_MIX_types_not_space();
}
```

#### Adding Data to a Vector
Vector push_back

Now that you are able to process a string, you may want to store the results of the processing in a convenient container for later use.   
现在您可以处理字符串，您可能希望将处理结果存储在方便的容器中以供以后使用。
In the next exercise, you will store the streamed ints from each line of the board in a vector<int>.   
在下一个练习中，您将在向量<int>中存储来自board每行的流式整数。
To do this, you will add the ints to the back of the vector, using he vector method    push_back:   
为此，您将使用向量方法push_back将int添加到向量的背面：

```c++
#include <vector>
#include <iostream>
using std::vector;
using std::cout;


/////////////////////
// push_back(data)
/////////////////////
int main() {
    // Initial Vector
    //vector<int> v {1, 2, 3};
    vector v {1, 2, 3}; //works only on c++17 without vector type

    // Print the contents of the vector
    for (int i=0; i < v.size(); i++) {
      cout << v[i] << "\n";
    }

    // Push 4 to the back of the vector
    v.push_back(4);

    // Print the contents again
    for (int i=0; i < v.size(); i++) {
      cout << v[i] << "\n";
    }

}
```

#### Parse Lines from the File
Now that you are able to read a board line by line from a file, you will want to parse these lines and store them in a `vector<int>`
```c++
#include <fstream>
#include <iostream>
#include <string>
#include <vector>
using std::cout;
using std::ifstream;
using std::string;
using std::vector;

//for String stream to INT
#include <sstream>
using std::istringstream;

// TODO: Add the ParseLine function here.
vector<int> ParseLine(string line){

    vector<int> rst;
    istringstream myrerader(line);
    char c;
    int n;
    while(myrerader>>n>>c){
        rst.push_back(n);
    }

    return rst;
}


void ReadBoardFile(string path) {
  ifstream myfile (path);
  if (myfile) {
    string line;
    while (getline(myfile, line)) {
      cout << line << "\n";
    }
  }
}

void PrintBoard(const vector<vector<int>> board) {
  for (int i = 0; i < board.size(); i++) {
    for (int j = 0; j < board[i].size(); j++) {
      cout << board[i][j];
    }
    cout << "\n";
  }
}

#include "test.cpp" // For testing.

int main() {
  ReadBoardFile("1.board");
  TestParseLine(); // For testing.
  // Leave commented out.
  // PrintBoard(board);
}
```

#### Use ParsLine Function
```c++
#include <fstream>
#include <iostream>
#include <string>
#include <sstream>
#include <vector>
using std::cout;
using std::ifstream;
using std::istringstream;
using std::string;
using std::vector;


vector<int> ParseLine_row(string line) {
    istringstream sline(line);
    int n;
    char c;
    vector<int> row;
    while (sline >> n >> c && c == ',') {
      row.push_back(n);
    }
    return row;
}

// TODO: Change the return type of ReadBoardFile.
vector<vector<int>> ReadBoardFile(string path) {
  ifstream myfile (path);
  // TODO: Declare an empty board variable here with
  // type vector<vector<int>>.
  vector<vector<int>> board;
  if (myfile) {
    string line;
    while (getline(myfile, line)) {
      // TODO: Replace the "cout" code with a call to ParseLine for each line and push the results of ParseLine to the back of the board.
      board.push_back(ParseLine_row(line));
      //cout << line << "\n";
    }
  }
  // TODO: Return the board variable.
  return board;
}

void PrintBoard(const vector<vector<int>> board) {
  for (int i = 0; i < board.size(); i++) {
    for (int j = 0; j < board[i].size(); j++) {
      cout << board[i][j];
    }
    cout << "\n";
  }
}

int main() {
  // TODO: Store the output of ReadBoardFile in the "board" variable.
  vector<vector<int>> board;
  board = ReadBoardFile("1.board");
  // TODO: Uncomment PrintBoard below to print "board".
  PrintBoard(board);
}
```

#### Formatting the Printed Board
 An enum, short for `enumerato`r, is a way to define a type in C++ with values that are restricted to a fixed range   
 enum是枚举器的缩写，是一种在C ++中定义类型的方法，其值限制在固定范围内
 In the previous exercises, you stored and printed the board as a vector<vector<int>>,where only two states were used for each cell: 0 and 1. This is a great way to get started,
but as the program becomes more complicated, there will be more than two possible states for each cell.   
在前面的练习中，您将board存储并打印为矢量<vector <int >>，   
每个单元只使用两个状态：0和1.这是一个很好的入门方式，
但随着程序变得更加复杂，每个单元格将有两种以上的可能状态。   
Additionally, it would be nice to print the board in a way that clearly indicates open areas and obstacles,
just as the board is printed above.   
此外，以明确指出开放区域和障碍物的方式打印board会很不错，就像上面印有board一样。

To do this clearly in your code, you will learn about and use something called an enum.
An enum, short for enumerator, is a way to define a type in C++ with values that are restricted to a fixed range.
For an explanation and examples, see the notebook below.   
要在代码中清楚地执行此操作，您将了解并使用称为枚举的内容。   
enum是枚举器的缩写，是一种在C ++中定义类型的方法，其值限制在固定范围内。有关说明和示例，请参阅下面的笔记本。

Enums
C++ allows you to define a custom type which has values limited to a specific range you list or "enumerate".   
This custom type is called an "enum".   
C ++允许您定义一个自定义类型，其值限制为您列出或“枚举”的特定范围。   
此自定义类型称为“枚举”。   

Suppose you were writing a program that stores information about each user's car, including the color.  
You could define a Color enum in your program, with a fixed range of all the acceptable values:   
假设您正在编写一个程序来存储有关每个用户汽车的信息，包括颜色。  
您可以在程序中定义Color枚举，其中包含所有可接受值的固定范围：   
We want to limited the possible colors.   
    white   
    black   
    blue  
    red   
https://en.cppreference.com/w/cpp/language/enum  

scoped enums  
    => enum + class/structure + name {items}  

unscoped enums (only remove the class/sturcture   from scoped enums)  
    => enum + name {items}   
    
```c++
#include <iostream>
using std::cout;

void scoped_enum(){
    // Create the enum Color with fixed values.
    // scoped enum
    enum class Color {white,
                      black,
                      blue,
                      red};

    // Create a Color variable and set it to Color::blue.
    Color my_color;
    //assign
    my_color = Color::blue;

    // Test to see if my car is red.
    if (my_color == Color::red) {
        cout << "The color of my car is red!" << "\n";
    } else {
        cout << "The color of my car is not red." << "\n";
    }
}

void unscoped_enum(){

    enum Color {  white =0,
                  black,
                  blue,
                  red};

    Color my_color = blue;
    cout << my_color << "\n";
    // Test to see if my car is red.
    if (my_color == red) {
        cout << "The color of my car is red!" << "\n";
    } else {
        cout << "The color of my car is not red." << "\n";
    }
}

void enum_switch(){

    enum class keypad {up,down,left,right};

    keypad input;
    input = keypad::down;

    switch(input){
        case keypad::up:
            cout<<"up"<<"\n";
            break;
        case keypad::down:
            cout<<"down"<<"\n";
            break;
        case keypad::left:
            cout<<"left"<<"\n";
            break;
        case keypad::right:
            cout<<"right"<<"\n";
            break;
    }
}

int main()
{
    scoped_enum();
    unscoped_enum();
    enum_switch();
}

```

#### Formatting the Printed Board
Formatting the Printed Board   
0   ⛰️   0   0   0   0    
0   ⛰️   0   0   0   0    
0   ⛰️   0   0   0   0   
0   ⛰️   0   0   0   0    
0   0    0   0  ⛰️   0   

The board will eventually have more than two cell states as the program becomes more complicated,   
and it would be nice to add formatting to the printed output of the board to ensure readability as the number of board states increases.    
随着程序变得更加复杂，最终将拥有两个以上的单元状态，
最好在board的打印输出上添加格式，以确保随着board状态数量的增加而增加可读性。    
To accommodate more board states and facilitate print formatting, we have provided the State enum with enumerator values kEmpty and kObstacle. In this exercise,you will write a CellString function which converts each State to an appropriate string.   
为了容纳更多的板状态并促进打印格式化，我们为State枚举提供了枚举值kEmpty和kObstacle。 在本练习中，您将编写一个CellString函数，该函数将每个State转换为适当的字符串。  
In the next exercise, we will update the program to use the enum values and CellString function.   
```c++
#include <fstream>
#include <iostream>
#include <sstream>
#include <string>
#include <vector>
using std::cout;
using std::ifstream;
using std::istringstream;
using std::string;
using std::vector;

enum class State {kEmpty, kObstacle};

vector<int> ParseLine(string line) {
    istringstream sline(line);
    int n;
    char c;
    vector<int> row;
    while (sline >> n >> c && c == ',') {
      row.push_back(n);
    }
    return row;
}

vector<vector<int>> ReadBoardFile(string path) {
  ifstream myfile (path);
  vector<vector<int>> board{};
  if (myfile) {
    string line;
    while (getline(myfile, line)) {
      vector<int> row = ParseLine(line);
      board.push_back(row);
    }
  }
  return board;
}

// TODO: Create the CellString function here,
// using the following return strings:
// "⛰️   "
// "0   "
void CellString(State cell){

    switch(cell){
        case State::kEmpty:
                return "0   ";
        case State::kObstacle:
                return "⛰️   ";
    }

}


void PrintBoard(const vector<vector<int>> board) {
  for (int i = 0; i < board.size(); i++) {
    for (int j = 0; j < board[i].size(); j++) {
      cout << board[i][j];
    }
    cout << "\n";
  }
}

int main() {
  auto board = ReadBoardFile("1.board");
  PrintBoard(board);
}

```

#### Store he Board using the State Enum
```c++
#include <fstream>
#include <iostream>
#include <sstream>
#include <string>
#include <vector>
using std::cout;
using std::ifstream;
using std::istringstream;
using std::string;
using std::vector;

enum class State {kEmpty, kObstacle};

// TODO: Change the return type to use auto or
// explicitly indicate vector<State>
vector<State> ParseLine(string line) {
    istringstream sline(line);
    int n;
    char c;
    // TODO: Change the variable type for row
    // to be a vector<State>
    vector<State> row;
    State curstate;
    while (sline >> n >> c && c == ',') {
      // TODO: Modify the line below to push_back
      // a State::kEmpty if n is 0, and push_back
      // a State::kObstacle otherwise.
      if (n==0){
          curstate = State::kEmpty;
      }else if(n==1){
          curstate = State::kObstacle;
      }

      row.push_back(curstate);
    }
    return row;
}

// TODO: Modify the return type here as well. Just
// as above, the board will contain State objects
// instead of ints.
vector<vector<State>> ReadBoardFile(string path) {
  ifstream myfile (path);
  // TODO: Modify the board declarationto store
  // State objects instead of ints.
  vector<vector<State>> board{};
  if (myfile) {
    string line;
    while (getline(myfile, line)) {
      // TODO: Modify the row type to use State
      // objects instead of ints.
      vector<State> row = ParseLine(line);
      board.push_back(row);
    }
  }
  return board;
}

string CellString(State cell) {
  switch(cell) {
    case State::kObstacle: return "⛰️   ";
    case State::kEmpty: return "0   ";
    //default: return "0   ";
  }
}

void PrintBoard(const vector<vector<State>> board) {
  for (int i = 0; i < board.size(); i++) {
    for (int j = 0; j < board[i].size(); j++) {
      // TODO: Modify the line below to call CellString
      // on each element of the board before streaming to cout.
      cout << CellString(board[i][j]);
    }
    cout << "\n";
  }
}

int main() {
  auto board = ReadBoardFile("1.board");
  PrintBoard(board);
}

```