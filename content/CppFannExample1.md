

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [FANN example 1: basics](CppFannExample1.htm)
==============================================================

 

This example demonstrates a basic [FANN](CppFann.htm) program.

 

-   [Download the Qt Creator project
    'CppFannExample1' (zip)](CppFannExample1.zip)

 

Operating system: [Ubuntu](http://www.ubuntu.com) 10.04 LTS Lucid Lynx

[IDE](CppIde.htm): [Qt Creator](CppQtCreator.htm) 2.0.0

[Project type](CppQtProjectType.htm): [GUI](CppGui.htm) application

[Compiler](CppCompiler.htm): [G++](CppGpp.htm) 4.4.1

[Libraries](CppLibrary.htm) used:

-   [FANN](CppFann.htm): version 1.2.0-1
-   [STL](CppStl.htm): from [GCC](CppGcc.htm), shipped with [Qt
    Creator](CppQt.htm) 2.0.0

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm)
---------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #------------------------------------------------- # # Project created by QtCreator 2010-08-12T16:17:45 # #------------------------------------------------- QT       += core QT       -= gui LIBS += -L/usr/local/lib -lfann TARGET = CppFannExample1 CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app SOURCES += main.cpp`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

main.cpp
--------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <vector>  #include <floatfann.h>  int main() {   //Create layer sizes { 2,2,1 }   std::vector<unsigned int> layer_sizes(2,2);   layer_sizes.push_back(1); //One output neuron    //Create the neural network from it   const double learning_rate = 0.05;   fann * const n = fann_create_shortcut_array(     learning_rate,     layer_sizes.size(),     &layer_sizes[0]);    //Create the inputs   std::vector<fann_type> inputs(2);   inputs[0] = 0.0;   inputs[1] = 1.0;    //Calculate the neural net output   fann_type * const outputs = fann_run(n, &inputs[0]);    //'The' output is just the one output neuron added at top   const double output = outputs[0];    std::cout << "Output: " << output << '\n';    //Destroy the network   fann_destroy(ann); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)