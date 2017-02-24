

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [TestLogicalOrVersusBitwiseOr](TestLogicalOrVersusBitwiseOr.htm)
=================================================================================

 

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./TestLogicalOrVersusBitwiseOr/TestLogicalOrVersusBitwiseOr.pro
--------------------------------------------------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------
  ` TEMPLATE = app CONFIG += console CONFIG -= app_bundle CONFIG -= qt  SOURCES += main.cpp`
  --------------------------------------------------------------------------------------------

 

 

 

 

 

./TestLogicalOrVersusBitwiseOr/main.cpp
---------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  int main() {   if (1  | (1/0)) { std::cout << "X"; }   if (1 || (1/0)) { std::cout << "Y"; }   if (!(0  & (1/0))) { std::cout << "A"; }   if (!(0 && (1/0))) { std::cout << "B"; }   std::cout << std::endl; }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)