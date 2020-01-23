### 1. Open Street Map Data

The OpenStreetMap data that you will be using for this project comes in the form of an OSM XML file (.osm file). A sample of an OSM XML file from the [OpenStreetMap Wiki](https://wiki.openstreetmap.org/wiki/Main_Page) is provided below. 

The XML file contains several element types which are important to the code you will be writing: Nodes, Ways, and Relations.

**Nodes** 

A *node* is one of the most basic elements in the OpenStreetMap data model. Each node indicates a single point with an identifier `id`, latitude `lat`, and longitude `lon`. There are other XML attributes in a node element that won't be relevant to this project, such as the `user` id and the `timestamp` when the node was added to the data set. Additionally, a node can have several tags which provide additional information. 

**Ways** 

A *way* is an ordered list of nodes that represents a feature in the map. This feature could be a road, or a boundary of a park, or some other feature in the map. Each way has at least one `tag` which denotes some information about the way, and each way also belongs to at least one relation, which is described below. 

**Relations** 

A *relation* is a data structure which documents a relationship between other data elements. Examples from the OpenStreetMap wiki include:

 - A route relation which lists the ways that form a major highway, cycle route, or bus route.
 - A multipolygon that describes an area with holes, where the outer and inner boundaries of the area are given by two ways. 



### 2. IO2D Starter Code

**main.cpp** 

The `main.cpp` controls the flow of the program, accomplishing four primary tasks:

- The OSM data is read into the program.

- A `RouteModel` object is created to store the OSM data in usable data structures.

- A `RoutePlanner` object is created using the `RouteModel`. This planner will eventually carry out the A* search on the model data and store the search results in the `RouteModel`.

- The `RouteModel` data is rendered using the IO2D library.

     

**model.h and model.cpp** 

These files come from the IO2D example code. They are used to define the data structures and methods that read in and store OSM data. OSM data is stored in a `Model` class which contains nested structs for Nodes, Ways, Roads, and other OSM objects. You will be extending this class in your project. 



**render.h and render.cpp**

These files from the IO2D example code take model data and render it on a map. We have modified these files slightly to include three extra methods which render the start point, end point, and path from the A* search. You won't need to work too much with these files, but you will uncomment the code to render the results of your search at some point. 



**route_model.h and route_model.cpp** 

These files contain class stubs which will be used to extend the `Model` and `Node` data structures from `model.h` and `model.cpp` using *class inheritance*. Remember that inheritance in this case will allow you to use all of the *public* methods and attributes of the `Model` and `Node` classes in the derived classes. You will be filling out the classes in `route_model.h` and `route_model.cpp` over the course of your project. 



**route_planner.h and route_planner.cpp** 

These files contain a class stub for a `RoutePlanner` class which accepts a `RouteModel` along with `start` and `end` coordinates. The `RouteModel` data, along with the start and end points will be used for A* search, which will be implemented in these files. Have a look a the video below for a brief overview of the contents. 



### 3. This Pointer 

```
// The Car class
class Car {
  public:
    // Method to print data.
    void PrintCarData() {
        cout << "The distance that the " << this->color << " car " << this->number << " has traveled is: " << this->distance << "\n";
    }

    // Method to increment the distance travelled.
    void IncrementDistance() {
        this->distance++;
    }

    // Class/object attributes
    string color;
    int distance = 0;
    int number;
};
```



### 4. Hash Tables

To create an unordered_map in C++, you must include the <unordered_map> header,
and the sytnax for declaring an unordered_map is as follows:

unordered_map <key_type, value_type> variable_name;
In the code below, we check if the key is in the unordered_map using the .find() method.
If the key does not exist in the map, then .find() returns an unordered_map::end() type.
Otherwise, .find() returns a C++ iterator, which is a pointer that points to the beginning of the iterable key-value pair.

```C++
#include <iostream>
#include <vector>
#include <unordered_map>
#include <string>
using std::vector;
using std::cout;
using std::unordered_map;
using std::string;

//using std::unordered_multimap;

void demo1(){
    // Create strings to use in the hash table.
    string key = "word";
    string def_1 = "a unit of language, consisting of one or more spoken sounds or their written representation, that functions as a principal carrier of meaning";
    string def_2 = "speech or talk: to express one's emotion in words";
    string def_3 = "a short talk or conversation: 'Marston, I'd like a word with you.'";
    string def_4 = "an expression or utterance: a word of warning";
    unordered_map <string, vector<string>> my_dictionary;

    // Check if key is in the hash table.
    if (my_dictionary.find(key) == my_dictionary.end()) {
        cout << "The key 'word' is not in the dictionary." << "\n";
        cout << "Inserting a key-value pair into the dictionary." << "\n\n";
        // Set the value for the key.
        my_dictionary[key] = vector<string> {def_1, def_2, def_3, def_4};
    }

    // The key should now be in the hash table. You can access the
    // value corresponding to the key with square brackets [].
    // Here, the value my_dictionary[key] is a vector of strings.
    // We iterate over the vector and print the strings.
    cout << key << ": \n";
    auto definitions = my_dictionary[key];
    for (string definition : definitions) {
        cout << definition << "\n";
    }
}

void country_code(){
    unordered_map<int, string>      IDD_codes { {972, "Israel"}, {93, "Afghanistan"}, {355, "Albania"}, {213, "Algeria"}, {376, "Andorra"},
                                                {244, "Angola"}, {54, "Argentina"}, {374, "Armenia"}, {297, "Aruba"}, {61, "Australia"},
                                                 {43, "Austria"}, {994, "Azerbaijan"}, {973, "Bahrain"},
                                                {880, "Bangladesh"}, {375, "Belarus"}, {32, "Belgium"}, {501, "Belize"}, {229, "Benin"},
                                                 {975, "Bhutan"}, {387, "Bosnia and Herzegovina"},
                                                {267, "Botswana"}, {55, "Brazil"}, {246, "British Indian Ocean Territory"}, {359, "Bulgaria"}, {226, "Burkina Faso"},
                                                {257, "Burundi"}, {855, "Cambodia"}, {237, "Cameroon"}, {1, "Canada"}, {238, "Cape Verde"}, {236, "Central African Republic"},
                                                {235, "Chad"}, {56, "Chile"}, {86, "China"}, {61, "Christmas Island"}, {57, "Colombia"}, {269, "Comoros"}, {242, "Congo"},
                                                {682, "Cook Islands"}, {506, "Costa Rica"}, {385, "Croatia"}, {53, "Cuba"}, {537, "Cyprus"}, {420, "Czech Republic"},
                                                {45, "Denmark"}, {253, "Djibouti"}, {593, "Ecuador"}, {20, "Egypt"}, {503, "El Salvador"}, {240, "Equatorial Guinea"},
                                                {291, "Eritrea"}, {372, "Estonia"}, {251, "Ethiopia"}, {298, "Faroe Islands"}, {679, "Fiji"},
                                                {358, "Finland"}, {33, "France"}, {594, "French Guiana"}, {689, "French Polynesia"}, {241, "Gabon"},
                                                {220, "Gambia"}, {995, "Georgia"}, {49, "Germany"}, {233, "Ghana"}, {350, "Gibraltar"}, {30, "Greece"},
                                                {299, "Greenland"}, {590, "Guadeloupe"}, {502, "Guatemala"}, {224, "Guinea"}, {245, "Guinea-Bissau"},
                                                {595, "Guyana"}, {509, "Haiti"}, {504, "Honduras"}, {36, "Hungary"}, {354, "Iceland"}, {91, "India"},
                                                {62, "Indonesia"}, {964, "Iraq"}, {353, "Ireland"}, {972, "Israel"}, {39, "Italy"},
                                                {81, "Japan"}, {962, "Jordan"}, {254, "Kenya"}, {686, "Kiribati"}, {965, "Kuwait"}, {996, "Kyrgyzstan"},
                                                {371, "Latvia"}, {961, "Lebanon"}, {266, "Lesotho"}, {231, "Liberia"}, {423, "Liechtenstein"}, {370, "Lithuania"},
                                                {352, "Luxembourg"}, {261, "Madagascar"}, {265, "Malawi"}, {60, "Malaysia"}, {223, "Mali"}, {356, "Malta"},
                                                {692, "Marshall Islands"}, {596, "Martinique"}, {222, "Mauritania"}, {230, "Mauritius"}, {262, "Mayotte"},
                                                {52, "Mexico"}, {377, "Monaco"}, {976, "Mongolia"}, {382, "Montenegro"}, {212, "Morocco"}, {95, "Myanmar"},
                                                {264, "Namibia"}, {674, "Nauru"}, {977, "Nepal"},
                                                {31, "Netherlands"}, {599, "Netherlands Antilles"}, {687, "New Caledonia"}, {64, "New Zealand"},
                                                {505, "Nicaragua"}, {227, "Niger"}, {234, "Nigeria"}, {683, "Niue"}, {672, "Norfolk Island"}, {47, "Norway"},
                                                {968, "Oman"}, {92, "Pakistan"}, {680, "Palau"}, {507, "Panama"}, {675, "Papua New Guinea"}, {595, "Paraguay"}, {51, "Peru"},
                                                {63, "Philippines"}, {48, "Poland"}, {351, "Portugal"}, {974, "Qatar"}, {40, "Romania"}, {250, "Rwanda"},
                                                {685, "Samoa"}, {378, "San Marino"}, {966, "Saudi Arabia"}, {221, "Senegal"}, {381, "Serbia"}, {248, "Seychelles"}, {232, "Sierra Leone"}, {65, "Singapore"}, {421, "Slovakia"}, {386, "Slovenia"}, {677, "Solomon Islands"}, {27, "South Africa"}, {500, "South Georgia and the South Sandwich Islands"}, {34, "Spain"}, {94, "Sri Lanka"}, {249, "Sudan"}, {597, "Suriname"},
                                                {268, "Swaziland"}, {46, "Sweden"}, {41, "Switzerland"}, {992, "Tajikistan"}, {66, "Thailand"}, {228, "Togo"}, {690, "Tokelau"}, {676, "Tonga"}, {216, "Tunisia"}, {90, "Turkey"}, {993, "Turkmenistan"}, {688, "Tuvalu"}, {256, "Uganda"}, {380, "Ukraine"},
                                                {971, "United Arab Emirates"}, {44, "United Kingdom"}, {1, "United States"}, {598, "Uruguay"}, {998, "Uzbekistan"},
                                                {678, "Vanuatu"}, {681, "Wallis and Futuna"}, {967, "Yemen"}, {260, "Zambia"}, {263, "Zimbabwe"},
                                                {591, "Bolivia, Plurinational State of"}, {673, "Brunei Darussalam"},
                                                {61, "Cocos (Keeling) Islands"}, {243, "Congo, The Democratic Republic of the"}, {225, "Cote dIvoire"},
                                                {500, "Falkland Islands (Malvinas)"}, {44, "Guernsey"}, {379, "Holy See (Vatican City State)"}, {852, "Hong Kong"},
                                                {98, "Iran, Islamic Republic of"}, {44, "Isle of Man"}, {44, "Jersey"}, {850, "Korea, Democratic People's Republic of"},
                                                {82, "Korea, Republic of"}, {856, "Lao People's Democratic Republic"}, {218, "Libyan Arab Jamahiriya"}, {853, "Macao"},
                                                {389, "Macedonia, The Former Yugoslav Republic of"}, {691, "Micronesia, Federated States of"}, {373, "Moldova, Republic of"},
                                                {258, "Mozambique"}, {970, "Palestinian Territory, Occupied"}, {872, "Pitcairn"}, {262, "Réunion"}, {7, "Russia"},
                                                {590, "Saint Barthélemy"}, {290, "Saint Helena, Ascension and Tristan Da Cunha"}, {590, "Saint Martin"},
                                                {508, "Saint Pierre and Miquelon"},
                                                {239, "Sao Tome and Principe"}, {252, "Somalia"}, {47, "Svalbard and Jan Mayen"}, {963, "Syrian Arab Republic"},
                                                {886, "Taiwan, Province of China"}, {255, "Tanzania, United Republic of"}, {670, "Timor-Leste"},
                                                {58, "Venezuela, Bolivarian Republic of"}, {84, "Viet Nam"}};

    cout << "total size: "<<IDD_codes.size() << "\n";
    //auto range = IDD_codes.equal_range(1);
    //for (auto iterator = range.first; iterator != range.second; ++iterator)
    //    cout << iterator->first << ": " << iterator->second << "\n";


    //check if the {960, "Maldives"} in the map or not
    //if not found, we add one
    if (IDD_codes.find(960) == IDD_codes.end()){
        IDD_codes[960] = "Maldives";
    }

    //testing some code
    vector<int> my_code {389,4,6,960};
    for (auto code : my_code){
        if(IDD_codes.find(code) != IDD_codes.end())
            cout<<"code:" <<code<<",value: "<< IDD_codes[code] << "\n";
        else{
            cout<<"code:" <<code<<" not in map" << "\n";
        }
    }


}

int main() {
    //demo1();
    country_code();
}

```



