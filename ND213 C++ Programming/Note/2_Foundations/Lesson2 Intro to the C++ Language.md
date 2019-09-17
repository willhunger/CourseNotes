[TOC]

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



### 5. Working With Vectors

```C++
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



### 6. Reading from a File

```C++
#include <iostream>
#include <string>
#include <vector>
using std::cout;
using std::string;
using std::vector;

#include <fstream>
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



### 7. Processing Strings

In C++ strings can be streamed into temporary variables, similarly to how files can be streamed into strings. Streaming a string allows us to work with each character individually.

在C++中，字符串流可以传输到临时变量中，类似的，文件也能串流到字符串中。构造字符串流允许我们单独处理每一个字符。

One way to stream a string is to use an input string stream object istringstream from the <sstream> header.

使用字符串流地一种方法是通过 <sstream> 头文件中的字符串流输入对象 istringstream 。

Once an istringstream object has been created, parts of the string can be streamed and stored using the "extraction operator": >>.

一旦 istringstream 对象被创建，就可以通过 提取运算符>>  操作。

The extraction operator will read until whitespace is reached or until the stream fails.

一旦遇到空或者流失败，提取运算符就会停止读取。

```c++
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



### 8. Adding Data to a Vector

```C++
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



### 9. Parse Lines from the File

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



### 10. Use the ParseLine Function

```C++
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



### 11. Enumerator

C++ allows you to define a custom type which has values limited to a specific range you list or "enumerate". This custom type is called an "enum". 

```c++
#include <iostream>
using std::cout;

/* 
Suppose you were writing a program that stores information about each user's car, including the color.
You could define a Color enum in your program, with a fixed range of all the acceptable values:

We want to limited the possible colors.

    white
    black
    blue
    red

https://en.cppreference.com/w/cpp/language/enum

scoped enums
    => enum + class/structure + name {items}

unscoped enums (only remove the class/sturcture from scoped enums)
    => enum + name {items}

*/


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



### 12. Store the Board Using the State Enum

```C++
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

