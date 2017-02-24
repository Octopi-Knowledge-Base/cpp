

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [SortExample1](CppSortExample1.htm)
====================================================

 

Technical facts
---------------

 

[Application type(s)](CppApplication.htm)

-   ![Desktop](PicDesktop.png) [Desktop
    application](CppDesktopApplication.htm)

[Operating system(s) or programming environment(s)](CppOs.htm)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.htm) 15.04 (vivid)

[IDE(s)](CppIde.htm):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.htm) 3.1.1

[Project type](CppQtProjectType.htm):

-   ![GUI](PicGui.png) [GUI application](CppGuiApplication.htm)

[C++ standard](CppStandard.htm):

-   ![C++11](PicCpp11.png) [C++11](Cpp11.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.9.2

[Libraries](CppLibrary.htm) used:

-   ![Qt](PicQt.png) [Qt](CppQt.htm): version 5.4.1 (32 bit)
-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppSortExample1/CppSortExample1.pro
------------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` # Go ahead and use Qt.Core: it is about as platform-independent as # the STL and Boost QT += core  # Go ahead and use Qt.Gui: it is about as platform-independent as # the STL and Boost. It is needed for QImage QT += gui  # Don't define widgets: it would defy the purpose of this console # application to work non-GUI #greaterThan(QT_MAJOR_VERSION, 4): QT += widgets  CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app  # # # Type of compile # #  CONFIG(release, debug|release) {   DEFINES += NDEBUG NTRACE_BILDERBIKKEL }  QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++  unix {   QMAKE_CXXFLAGS += -Werror }  SOURCES += main.cpp  win32 {   INCLUDEPATH += \     ../../Libraries/boost_1_54_0 }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppSortExample1/main.cpp
--------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/bind.hpp> #include <boost/lambda/lambda.hpp> #pragma GCC diagnostic pop  void AbsSortBoost(std::vector<int>& v) noexcept {   std::sort(     v.begin(),     v.end(),       boost::bind(&std::labs,boost::lambda::_1)     < boost::bind(&std::labs,boost::lambda::_2)   ); }  void AbsSortLambda(std::vector<int>& v) noexcept {   std::sort(     v.begin(),     v.end(),     [](const int a, const int b) { return std::abs(a) < std::abs(b); }   ); }  int main() {   for (const auto f: { AbsSortBoost, AbsSortLambda } )   {     std::vector<int> v = { 4,-3,2,-1 };     f(v);     assert(v[0] == -1);     assert(v[1] ==  2);     assert(v[2] == -3);     assert(v[3] ==  4);   } }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)