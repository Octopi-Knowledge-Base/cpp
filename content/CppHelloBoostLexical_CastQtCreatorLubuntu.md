
 

 

 

 

 

([C++](Cpp.md)) [HelloBoostLexical\_CastQtCreatorLubuntu](CppHelloBoostLexical_CastQtCreatorLubuntu.md)
=========================================================================================================

 

![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[Hello Boost.Lexical\_cast using Qt Creator under
Lubuntu](CppHelloBoostLexical_CastQtCreatorLubuntu.md) is a [Hello
Boost.Lexical\_cast](CppHelloBoostLexical_Cast.md) program.

 

-   [Download the Qt Creator project
    'CppHelloBoostLexical\_CastQtCreatorLubuntu' (zip)](CppHelloBoostLexical_CastQtCreatorLubuntu.zip)

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1

[Project type](CppQtProjectType.md):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)

[C++ standard](CppStandard.md):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppHelloBoostLexical\_CastQtCreatorLubuntu/CppHelloBoostLexical\_CastQtCreatorLubuntu.pro
------------------------------------------------------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppHelloBoostLexical\_CastQtCreatorLubuntu/main.cpp
-----------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/lexical_cast.hpp> #pragma GCC diagnostic pop  int main() {   const int x = 110;   const int y = 0;   const int z = 1;   const std::string s     = std::string("He")     + boost::lexical_cast<std::string>(x)     + std::string(" w")     + boost::lexical_cast<std::string>(y)     + std::string("r")     + boost::lexical_cast<std::string>(z)     + std::string("d");   std::cout << s << '\n'; }  /* Screen output:  He110 w0r1d  */`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppHelloBoostLexical\_CastQtCreatorLubuntu/CppHelloBoostLexical\_CastQtCreatorLubuntu.sh
------------------------------------------------------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #!/bin/bash myfile="qmake" mytarget="CppHelloBoostLexical_CastQtCreatorLubuntu" myprofile=$mytarget.pro   if [ ! -e $myprofile ] then   echo "Qt Creator project '$myprofile' not found"   exit fi  $myfile $myprofile  if [ ! -e Makefile ] then   echo "FAIL: $myfile $myprofile"   exit fi  make  if [ -e $mytarget ] then   echo $mytarget": SUCCESS" else   echo $mytarget": FAIL" fi  #Cleaning up rm *.o rm Makefile rm $mytarget`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

