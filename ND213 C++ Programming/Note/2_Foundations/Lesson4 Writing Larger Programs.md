### 1. Header Files

Header files, or `.h` files, allow related function, method, and class declarations to be collected in one place. The corresponding definitions can then be placed in `.cpp` files. The compiler considers a header declaration a "promise" that the definition will be found later in the code, so if the compiler reaches a function that hasn't been defined yet, it can continue on compiling until the definition is found. This allows functions to be defined (and declared) in arbitrary order.

```C++
//include guard
#ifndef HEADER_EXAMPLE_H
#define HEADER_EXAMPLE_H

//don't need variable names, just variable types.
void OuterFunction(int);
void InnerFunction(int);

#endif

/*
NOTE:
The function declarations in the header file don't need variable names, just variable types.
You can put names in the declaration, however, and doing this often makes the code easier to read.
The #include statement for the header used quotes " " around the file name, and not angle brackets <>.
We have stored the header in the same directory as the .cpp file, and the quotes tell the preprocessor
to look for the file in the same directory as the current file - not in the usual set of directories where libraries are typically stored.

Finally, there is a preprocessor directive:
    #ifndef HEADER_EXAMPLE_H
    #define HEADER_EXAMPLE_H
at the top of the header, along with an #endif at the end. This is called an "include guard".
Since the header will be included into another file, and #include just pastes contents into a file,
the include guard prevents the same file from being pasted multiple times into another file.
This might happen if multiple files include the same header, and then are all included into the same main.cpp, for example.
The ifndef checks if HEADER_EXAMPLE_H has not been defined in the file already. If it has not been defined yet,
then it is defined with #define HEADER_EXAMPLE_H, and the rest of the header is used. If HEADER_EXAMPLE_H has already been defined,
then the preprocessor does not enter the ifndef block. Note: There are other ways to do this.
Another common way is to use an #pragma oncepreprocessor directive, but we won't cover that in detail here. See this Wikipedia article for examples.

*/

```



### 2. CMake and Make

In the previous notebook, you saw how example code could be split into multiple `.h` and `.cpp` files, and you used `g++` to build all of the files together. For small projects with a handful of files, this works well. But what would happen if there were hundreds, or even thousands, of files in the project? If these files were spread across many directories, it would be difficult to type all of the directory names on the command line each time, and if you wanted to make a small change to just a single file, you probably wouldn't want to recompile every file in the project.

Fortunately, there is a solution to this. Many larger C++ projects use a [build system](https://en.wikipedia.org/wiki/List_of_build_automation_software) to manage all the files during the build process. The build system allows for large projects to be compiled with a few commands, and build systems are able to do this in an efficient way by only recompiling files that have been changed.

In the notebook below you will learn a little more about what actually happens when you run `g++` with multiple files, and we will introduce `cmake` (and `make`), a build system which is popular in [large C++ projects](https://cmake.org/success/).  

* CMake and Make
    CMake is an open-source, platform-independent build system. CMake uses text documents, labeled as CMakeLists.txt files,to manage platform-specific build environments, like make.

    Unfortunately, an in-depth tutorial on CMake is beyond the scope of this course,
    but we can discuss the basics of how CMake works, so you will be ready to use it in your project.

* CMakeLists.txt
    CMakeList.txt files have a hierarchical structure, and one CMakeList.txt file can be included in each directory of the project.
    These files can be used to specify the locations of necessary packages, set build flags and environment variables, specify build target names and locations, and other actions.

* CMake Project
    A typical CMake project will have a top-level CMakeLists.txt and a build directory. From within the build directory, you could run

    root@abc123defg:/my_project/build# cmake ..
    root@abc123defg:/my_project/build# make


    The first line directs the cmake command at the top-level CMakeLists.txt file with ...
    This command uses the top-level CMakeLists.txt to configure the project and create a Makefile.
    
    In the second line, make finds the Makefile and uses the instructions in the Makefile to build the project.
    
    In general, CMake only needs to be run once for a project, unless you are changing build options (e.g. using different build flags).
    Make will be able to keep track of which files have changed and compile only those that need to be before building.

```C++
/*
Object Files
So far in this course, we have refered to running g++ as "compiling".

However, g++ performs several distinct tasks:

    1.The preprocessor runs and executes any statement beginning with a hash symbol: #.
        This takes care of any #include statements, for example, so that all code is in place and ready to compile.
    2.Each file in the source code is compiled into an "object file" (a .o file). Object files are platform-specific machine code that will be used to create an executable.
    3.The object files are "linked" together to make a single executable. In the examples you have seen so far, this executable is a.out, but you can specify whatever name you want.

    It is possible to have g++ perform each of the steps separately by using the -c flag.

        g++ -c main.cpp

    will produce a main.o file, and that file can be converted to an executable with

        g++ main.o


Try these commands in the terminal below:

Save the file. The button will save the file as main.cpp
Compile to an object file using the -c flag. You can list the files in the directory with ls.
After compiling, you should see a main.o somewhere in the directory (along with all the notebook files).

Convert the file to an executable with g++.
Run the executable with ./a.out.

*/


#include <iostream>
using std::cout;

int main()
{
    cout << "Hello!" << "\n";
}


/*
Compiling One File of Many

In the example above, you compiled a single source code file to an object file. That object file was then converted into an executable.
If you wanted to do this with many source code files, and your directory only contained the files for your project, your bash commands might look like the following:

root@abc123defg:/home/workspace# g++ -c *.cpp
root@abc123defg:/home/workspace# g++ *.o
root@abc123defg:/home/workspace# ./a.out
Here, the * operator is a wildcard, so any matching file is selected.

But what if you make changes to the code? In that case, you can compile only that file, and use the existing object files from the other source
files for linking. For example, if you only changed file_3.cpp in your code, and all other object files were already created, you could run:

root@abc123defg:/home/workspace# g++ -c file_3.cpp
root@abc123defg:/home/workspace# g++ *.o
root@abc123defg:/home/workspace# ./a.out
As mentioned previously, this works great for small programs, where all the files are easy to find, and you can remember
which ones you have modified. For larger projects, it is helpful to use a build system which can compile the right files for you and take care of linking.

*/

```



### 3. References

```C++
/*
References

As mentioned previously, a reference is another name given to an existing variable.
On the left hand side of any variable declaration, the & operator can be used to declare a reference.
*/


#include <iostream>
using std::cout;

int main()
{
    int i = 1;

    // Declare a reference to i.
    int& j = i;

    //check address
    cout << "i address: " << &i <<",j address: "<< &j<<"\n";

    cout << "The value of j is: " << j << "\n";

    // Change the value of i.
    i = 5;
    cout << "The value of i is changed to: " << i << "\n";
    cout << "The value of j is now: " << j << "\n";

    // Change the value of the reference.
    // Since reference is just another name for the variable,
    // th
    j = 7;
    cout << "The value of j is now: " << j << "\n";
    cout << "The value of i is changed to: " << i << "\n";
}
```



### 4. Pointers

*A C++ pointer is just a variable that stores the memory address of an object in your program.*

That is the most important thing to understand and remember about pointers - they essentially keep track of *where* a variable is stored in the computer's memory.

In the previous lessons, you implemented A* search in a single file without using C++ pointers, except in `CellSort` code that was provided for you; a C++ program can be written without using pointers extensively (or at all). However, pointers give you better control over how your program uses memory. However, much like the pass-by-reference example that you saw previously, it can often be far more efficient to perform an operation with a pointer to an object than performing the same operation using the object itself.

Pointers are an extremely important part of the C++ language, and as you are exposed to more C++ code, you will certainly encounter them. In this notebook, you will become familiar with basic pointers so you get comfortable with the syntax, and you will be ready to use them in the course project code.

```C++
/*
Accessing a Memory Address
Each variable in a program stores its contents in the computer's memory, and each chunk of the memory has an address number.
For a given variable, the memory address can be accessed using an ampersand in front of the variable.
To see an example of this, execute the following code which displays the hexadecimal memory addresses of the variables i and j:
*/

#include <iostream>
using std::cout;

int Accessing_Memory_Address() {
    cout<< __func__ <<"\n";
    int i = 5;
    int j = 6;

    // Print the memory addresses of i and j
    cout << "The address of i is: " << &i << "\n";
    cout << "The address of j is: " << &j << "\n";
}


/*
At this point, you might be wondering why the same symbol & can be used to both access memory addresses and,
as you've seen before, pass references into a function. This is a great thing to wonder about.
The overloading of the ampersand symbol & and the * symbol probably contribute to much of the confusion around pointers.

    The symbols & and * have a different meaning, depending on which side of an equation they appear.

This is extremely important to remember. For the & symbol, if it appears on the left side of an equation
(e.g. when declaring a variable), it means that the variable is declared as a reference.
If the & appears on the right side of an equation, or before a previously defined variable, 
it is used to return a memory address, as in the example above.


Try using the cell above to create new variables and print out their addresses!

*/


void Storing_Memory_Address_int(){
    cout<< __func__ <<"\n";

    int i = 5;
    // A pointer pointer_to_i is declared and initialized to the address of i.
    int* pointer_to_i = &i;

    // Print the memory addresses of i and j 
    cout << "The address of i is:          " << &i << "\n";
    cout << "The variable pointer_to_i is: " << pointer_to_i << "\n";
    cout << "The address of variable pointer_to_i is: " << &pointer_to_i << "\n";
    //Getting an Object Back from a Pointer Address : de-reference
    cout << "The value of variable pointer_to_i is: " << *pointer_to_i << "\n";
}

void change_value_by_pointer(){
    int i = 5;
    // A pointer pointer_to_i is declared and initialized to the address of i.
    int* pointer_to_i = &i;

    // Print the memory addresses of i and j
    cout << "The address of i is:          " << &i << "\n";
    cout << "The variable pointer_to_i is: " << pointer_to_i << "\n";

    // The value of i is changed.
    i = 7;
    cout << "The new value of the variable i is                     : " << i << "\n";
    cout << "The value of the variable pointed to by pointer_to_i is: " << *pointer_to_i << "\n";
}


int main(){
    Accessing_Memory_Address();
    Storing_Memory_Address_int();
    change_value_by_pointer();
}
```



### 5. Pointers Continued

```C++
/*
Pointers to Other Object Types
Although the type of object being pointed to must be included in a pointer declaration,
pointers hold the same kind of value for every type of object:

just a memory address to where the object is stored.

In the following code, a vector is declared.

Write your own code to create a pointer to the address of that vector.
Then, dereference your pointer and print the value of the first item in the vector.
*/

#include <iostream>
#include <vector>
using std::cout;
using std::vector;

void pointers_to_objects(){
    cout<< __func__ <<"\n";

    // Vector v is declared and initialized to {1, 2, 3}
    vector<int> v {1, 2, 3};

    // Declare and initialize a pointer to the address of v here:
    vector<int> *pointer_to_v;
    pointer_to_v = &v;

    // The following loops over each int a in the vector v and prints.
    // Note that this uses a "range-based" for loop:
    // https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Res-for-range
    for (int a: v) {
        cout << a << "\n";
    }

    // Dereference your pointer to v and print the int at index 0 here (note: you should print 1):
    for (int i=0; i<v.size();++i) {
        cout << (*pointer_to_v)[i]<< "\n";
    }
    // Dereference your pointer to v and print the int at index 0 here (note: you should print 1):
    cout << "The first element of v is: " << (*pointer_to_v)[0] << "\n";

}


void AddOne(int* j)
{
    // Dereference the pointer and increment the int being pointed to.
    (*j)++;

    /*
        When using pointers with functions, some care should be taken.
        If a pointer is passed to a function and then assigned to a variable in the function
        that goes out of scope after the function finishes executing, then the pointer
        will have undefined behavior at that point - the memory it is pointing to might be overwritten by other parts of the program.
    */
}

void Passing_Pointers_to_Function(){
    cout<< __func__ <<"\n";

    int i = 1;
    cout << "The value of i is: " << i << "\n";

    // Declare a pointer to i:
    int* pi = &i;
    AddOne(pi);
    cout << "The value of i is now: " << i << "\n";

}


//pass reference , name is j
int* AddOne(int& j)
{
    // Increment the referenced int and return the
    // address of j.
    j++;
    cout << "The address of j is: " << &j << "\n";

    return &j;
}


void Returning_Pointer_from_Function(){
    cout<< __func__ <<"\n";

    int i = 1;
    cout << "The value of i is: " << i << "\n";

    // Declare a pointer and initialize to the value
    // returned by AddOne:

    int* my_pointer = AddOne(i);
    cout << "The value of i is now: " << i << "\n";
    cout << "The value of the int pointed to by my_pointer is: " << *my_pointer << "\n";
    //check addr
    cout << "The address of i is: " << &i << "\n";
    cout << "The value of my_pointer is: " << my_pointer << "\n";
    // my_pointer has its own addr
    cout << "The addr of my_pointer is: " << &my_pointer << "\n";

}

int main(){
    pointers_to_objects();
    Passing_Pointers_to_Function();
    Returning_Pointer_from_Function();
}
```



### 6. References vs Pointers

Pointers and references can have similar use cases in C++. As seen previously both references and pointers can be used in pass-by-reference to a function. Additionally, they both provide an alternative way to access an existing variable: pointers through the variable's address, and references through another name for that variable. But what are the differences between the two, and when should each be used? The following list summarizes some of the differences between pointers and references, as well as when each should be used:

* References：
    * References must be initialized when they are declared. This means that a reference will always point to data that was intentionally assigned to it. 
    * References can not be null. This means that a reference should point to meaningful data in the program. 
    * When used in a function for pass-by-reference, the reference can be used just as a variable of the same type would be.
* Pointers：
    * Pointers can be declared without being initialized, which is dangerous. If this happens mistakenly, the pointer could be pointing to an arbitrary address in memory, and the data associated with that address could be meaningless, leading to undefined behavior and difficult-to-resolve bugs.
    * Pointers can be null. In fact, if a pointer is not initialized immediately, it is often best practice to initialize to `nullptr`, a special type which indicates that the pointer is null. 
    * When used in a function for pass-by-reference, a pointer must be dereferenced in order to access the underlying object. 



References are generally easier and safer than pointers. As a decent rule of thumb, references should be used in place of pointers when possible.

However, there are times when it is not possible to use references. One example is object initialization. You might like one object to store a reference to another object. However, if the other object is not yet available when the first object is created, then the first object will need to use a pointer, not a reference, since a reference cannot be null. The reference could only be initialized once the other object is created. 



### 7. Classes and Object-Oriented Programming

In C++ the attributes and methods that make up an object are specified in a code *class*, and each object in the program is an *instance* of that class. 

```C++
#include <iostream>
#include <string>
using std::string;
using std::cout;

// The Car class
class Car {
  public:
    // Method to print data.
    void PrintCarData()
    {
        cout << "The distance that the " << color << " car " << number << " has traveled is: " << distance << "\n";
    }

    // Method to increment the distance travelled.
    void IncrementDistance()
    {
        distance++;
    }

    // Class/object attributes
    string color;
    int distance = 0;
    int number;
};

int main()
{
    // Create class instances for each car.
    Car car_1, car_2, car_3;

    // Set each instance's color.
    car_1.color = "green";
    car_2.color = "red";
    car_3.color = "blue";

    // Set each instance's number.
    car_1.number = 1;
    car_2.number = 2;
    car_3.number = 3;

    // Increment car_1's position by 1.
    car_1.IncrementDistance();

    // Print out the position and color of each car.
    car_1.PrintCarData();
    car_2.PrintCarData();
    car_3.PrintCarData();

}
```


```C++
/*
Adding a Constructor
The best way to fix this is to add a constructor to the Car class.
The constructor allows you to instantiate new objects with the data that you want.
In the next code cell, we have added a constructor for Car that allows the number and color to be passed in.
This means that each Car object can be created with those variables.
*/

#include <iostream>
#include <string>
using std::string;
using std::cout;

class Car {
  public:
    void PrintCarData()
    {
        cout << "The distance that the " << color << " car " << number << " has traveled is: " << distance << "\n";
    }

    void IncrementDistance()
    {
        distance++;
    }

    // Adding a constructor here:
    Car(string c, int n)
    {
        // Setting the class attributes with
        // The values passed into the constructor.
        color = c;
        number = n;
    }

    string color;
    int distance = 0;
    int number;
};

int main()
{
    // Create class instances for each car.
    Car car_1 = Car("green", 1);
    Car car_2 = Car("red", 2);
    Car car_3 = Car("blue", 3);

    // Increment car_1's position by 1.
    car_1.IncrementDistance();

    // Print out the position and color of each car.
    car_1.PrintCarData();
    car_2.PrintCarData();
    car_3.PrintCarData();
}

/*
This is now beginning to look better. 
The main is more organized than when we first started, 
although there is a little more code overall to accomodate the class definition. 
At this point, you might want to separate your class definition into it's own .h and .cpp files. 
We'll do that in the next concept!
*/

```

**Inheritance** 

It is possible for a class to use methods and attributes from another class using class *inheritance*. For example, if you wanted to make a `Sedan` class with additional attributes or methods not found in the generic `Car` class, you could create a `Sedan` class that inherited from the `Car` by using the colon notation: 

```C++
class Sedan : public Car {
    // Sedan class declarations/definitions here.
};
```

By doing this, each `Sedan` class instance will have access to any of the *public* methods and attributes of `Car`. In the code above, these are`IncrementDistance()` and `PrintCarData()`. You can add additional features to the `Sedan` class as well. In the example above, `Car` is often referred to as the *parent* class, and `Sedan` as the *child* or *derived* class. 



### 8. Classes and OOP Continued

```C++
void Putting_Class_Definitions_into_Separate_Files(){
    // Create class instances for each car.
    Car car_1 = Car("green", 1);
    Car car_2 = Car("red", 2);
    Car car_3 = Car("blue", 3);

    // Increment car_1's position by 1.
    car_1.IncrementDistance();

    // Print out the position and color of each car.
    car_1.PrintCarData();
    car_2.PrintCarData();
    car_3.PrintCarData();
}


void scall_up_to_see_the_good_OOP(){
    // Create an empty vector of pointers to Cars
    // and a null pointer to a car.
    vector<Car*> car_vect;
    Car* cp = nullptr;

    // The vector of colors for the cars:
    vector<string> colors {"red", "blue", "green"};

    // Create 100 cars with different colors and
    // push pointers to each of those cars into the vector.
    for (int i=0; i < 100; i++) {;
        cp = new Car(colors[i%3], i+1);
        car_vect.push_back(cp);
    }

    // Move each car forward by 1.
    for (Car* cp: car_vect) {
        cp->IncrementDistance();
    }

    // Print data about each car.
    for (Car* cp: car_vect) {
        cp->PrintCarData();
    }
}
```



