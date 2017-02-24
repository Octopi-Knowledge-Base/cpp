

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [BoostUblasMatrixExample2](CppBoostUblasMatrixExample2.htm)
============================================================================

 

![Boost](PicBoost.png)

 

[boost::ublas::matrix example 2](CppBoostUblasMatrixExample2.htm) is a
[boost::ublas::matrix](CppBoostUblasMatrix.htm)
[example](CppExample.htm).

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

-   ![C++98](PicCpp98.png) [C++98](Cpp98.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.9.2

[Libraries](CppLibrary.htm) used:

-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppBoostUblasMatrixExample2/CppBoostUblasMatrixExample2.pro
------------------------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++1y -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostUblasMatrixExample2/main.cpp
--------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <boost/numeric/ublas/matrix.hpp>   const boost::numeric::ublas::matrix<int> CreateMatrix(const int n_cols, const int n_rows) {   boost::numeric::ublas::matrix<int> m(n_rows,n_cols); //y-x-ordered   for (int y = 0; y != n_rows; ++y)   {     for (int x = 0; x != n_cols; ++x)     {       m(y,x) = (y * 10) + x;     }   }   return m; }  int main() {   const int n_cols = 3;   const int n_rows = 2;   const boost::numeric::ublas::matrix<int> m = CreateMatrix(n_cols,n_rows);    //boost::numeric::ublas::matrix is y-x-ordered   assert(m(0,0) ==  0); assert(m(0,1) ==  1); assert(m(0,2) ==  2);   assert(m(1,0) == 10); assert(m(1,1) == 11); assert(m(1,2) == 12);    //Transpose   const boost::numeric::ublas::matrix<int> n = boost::numeric::ublas::trans(m);   assert(n(0,0) ==  0); assert(n(0,1) == 10);   assert(n(1,0) ==  1); assert(n(1,1) == 11);   assert(n(2,0) ==  2); assert(n(2,1) == 12); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)