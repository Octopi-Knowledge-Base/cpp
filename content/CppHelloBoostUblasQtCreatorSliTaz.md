

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [HelloBoostUblasQtCreatorSliTaz](CppHelloBoostUblasQtCreatorSliTaz.htm)
========================================================================================

 

![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![SliTaz](PicSliTaz.png)

 

[Hello Boost.uBLAS using Qt Creator under
SliTaz](CppHelloBoostUblasQtCreatorSliTaz.htm) is a [Hello
Boost.uBLAS](CppHelloBoostUblas.htm) program.

 

-   [Download the Qt Creator project
    'CppHelloBoostUblasQtCreatorSliTaz' (zip)](CppHelloBoostUblasQtCreatorSliTaz.zip)

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppHelloBoostUblasQtCreatorSliTaz/CppHelloBoostUblasQtCreatorSliTaz.pro
------------------------------------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppHelloBoostUblasQtCreatorSliTaz/main.cpp
--------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/numeric/ublas/matrix.hpp> #include <boost/numeric/ublas/io.hpp> #pragma GCC diagnostic pop  int main() {   const int n_cols = 2;   const int n_rows = 3;   {     boost::numeric::ublas::matrix<int> m(n_rows,n_cols);     assert(n_rows == static_cast<int>(m.size1()));     assert(n_cols == static_cast<int>(m.size2()));     for (int y = 0; y != n_rows; ++y)     {       for (int x = 0; x != n_cols; ++x)       {         m(y,x) = (y * 10) + x;       }     }     std::cout << m << std::endl;     assert(m(0,0) ==  0); assert(m(0,1) ==  1);     assert(m(1,0) == 10); assert(m(1,1) == 11);     assert(m(2,0) == 20); assert(m(2,1) == 21);   }   {     boost::numeric::ublas::matrix<int,boost::numeric::ublas::column_major> m(n_cols,n_rows);     assert(n_cols == static_cast<int>(m.size1()));     assert(n_rows == static_cast<int>(m.size2()));     for (int x = 0; x != n_cols; ++x)     {       for (int y = 0; y != n_rows; ++y)       {         m(x,y) = (y * 10) + x;       }     }     std::cout << m << std::endl;     assert(m(0,0) ==  0); assert(m(1,0) ==  1);     assert(m(0,1) == 10); assert(m(1,1) == 11);     assert(m(0,2) == 20); assert(m(1,2) == 21);   } }  /*  [3,2]((0,1),(10,11),(20,21)) [2,3]((0,10,20),(1,11,21))  */`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppHelloBoostUblasQtCreatorSliTaz/CppHelloBoostUblasQtCreatorSliTaz.sh
------------------------------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #!/bin/bash myfile="qmake" mytarget="CppHelloBoostUblasQtCreatorSliTaz" myprofile=$mytarget.pro   if [ -e $myfile ] then   echo "Compiler '$myfile' found" else   echo "Compiler '$myfile' not found directly"   #exit fi  if [ -e $myprofile ] then   echo "Qt Creator project '$myprofile' found" else   echo "Qt Creator project '$myprofile' not found"   exit fi  echo "1/2: Creating makefile"  $myfile $myprofile  if [ -e Makefile ] then   echo "Makefile created successfully" else   echo "FAIL: $myfile $myprofile"   exit fi  echo "2/2: Making makefile"  make  if [ -e $mytarget ] then   echo "SUCCESS" else   echo "FAIL" fi  #Cleaning up rm *.o rm Makefile rm $mytarget`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)