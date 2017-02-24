

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [TemplateFunctionExample1](CppTemplateFunctionExample1.htm)
============================================================================

 

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.htm)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.htm) 15.04 (vivid)

[IDE(s)](CppIde.htm):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.htm) 3.1.1

[Project type](CppQtProjectType.htm):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.htm)

[C++ standard](CppStandard.htm):

-   ![C++11](PicCpp11.png) [C++11](Cpp11.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.9.2

[Libraries](CppLibrary.htm) used:

-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppTemplateFunctionExample1/CppTemplateFunctionExample1.pro
------------------------------------------------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` TEMPLATE = app CONFIG += console CONFIG -= app_bundle CONFIG -= qt  SOURCES += main.cpp  CONFIG(release, debug|release) {   DEFINES += NDEBUG }  QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++  unix {   QMAKE_CXXFLAGS += -Werror }  win32 {   INCLUDEPATH += \     ../../Libraries/boost_1_54_0 }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppTemplateFunctionExample1/main.cpp
--------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` int AbsInt(const int n) { return n < 0 ? -n : n; }  double AbsDouble(const double n) { return (n < 0 ? -n : n); }  template <class T> T Abs(const T n) { return n < 0 ? -n : n; }  #include <cassert> #include <cmath>  int main() {   const double pi = M_PI;    assert(AbsInt( 42) == 42);   assert(AbsInt(-42) == 42);   assert(AbsDouble( pi) == pi);   assert(AbsDouble(-pi) == pi);    assert(Abs( 42) == 42);   assert(Abs(-42) == 42);   assert(Abs( pi) == pi);   assert(Abs(-pi) == pi); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)