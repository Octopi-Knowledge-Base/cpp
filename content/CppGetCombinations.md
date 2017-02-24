

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [GetCombinations](CppGetCombinations.htm)
==========================================================

 

![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[GetCombinations](CppGetCombinations.htm) is a [code
snippet](CppCodeSnippets.htm) to obtain all combinations of a
[std::vector](CppVector.htm).

 

[GetPermutations](CppGetPermutations.htm) is a [code
snippet](CppCodeSnippets.htm) to obtain all permutations of a
[std::vector](CppVector.htm).

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppGetCombinations/CppGetCombinations.pro
------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppGetCombinations/main.cpp
-----------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector>  ///Obtain all possible selections of a std::vector, preserving the ordering of its elements ///Examples: /// {     } -> { {}                                              } /// {1    } -> { {}, {1}                                         } /// {1,2  } -> { {}, {1}, {2},      {1,2}                        } /// {1,2,3} -> { {}, {1}, {2}, {3}, {1,2}, {1,3}, {2,3}, {1,2,3} } //From http://www.richelbilderbeek.nl/CppGetCombinations.htm template <class T> const std::vector<std::vector<T> > GetCombinations(const std::vector<T>& v) {   std::vector<std::vector<T> > result;   const int sz = static_cast<int>(v.size());   const int n_combinations = (1 << sz);    for (int i=0; i!=n_combinations; ++i)   {     std::vector<T> w;     for (int j=0; j!=sz; ++j)     {       if ((1 << j) & i)       {         w.push_back(v[j]);       }     }     result.push_back(w);   }   return result; }  #include <algorithm> #include <cassert>  int main() {   //Assume the number of elements is correct   assert(GetCombinations(std::vector<int>( {         } ) ).size() ==  1);   assert(GetCombinations(std::vector<int>( {1        } ) ).size() ==  2);   assert(GetCombinations(std::vector<int>( {1,2      } ) ).size() ==  4);   assert(GetCombinations(std::vector<int>( {1,2,3    } ) ).size() ==  8);   assert(GetCombinations(std::vector<int>( {1,2,3,4  } ) ).size() == 16);   assert(GetCombinations(std::vector<int>( {1,2,3,4,5} ) ).size() == 32);   //Assume the elements are correct   {     const std::vector<std::vector<int> > v = GetCombinations(std::vector<int>( { 1 } ) );     const std::vector<int> expected_0 = {};     const std::vector<int> expected_1 = {1};     assert(std::count(v.begin(),v.end(),expected_0));     assert(std::count(v.begin(),v.end(),expected_1));   }   {     const std::vector<std::vector<int> > v = GetCombinations(std::vector<int>( { 1,2 } ) );     const std::vector<int> expected_0 = {};     const std::vector<int> expected_1 = {1};     const std::vector<int> expected_2 = {2};     const std::vector<int> expected_3 = {1,2};     assert(std::count(v.begin(),v.end(),expected_0));     assert(std::count(v.begin(),v.end(),expected_1));     assert(std::count(v.begin(),v.end(),expected_2));     assert(std::count(v.begin(),v.end(),expected_3));   }   {     const std::vector<std::vector<int> > v = GetCombinations(std::vector<int>( { 1,2,3 } ) );     const std::vector<int> expected_0 = {};     const std::vector<int> expected_1 = {1};     const std::vector<int> expected_2 = {2};     const std::vector<int> expected_3 = {3};     const std::vector<int> expected_4 = {1,2};     const std::vector<int> expected_5 = {1,3};     const std::vector<int> expected_6 = {2,3};     const std::vector<int> expected_7 = {1,2,3};     assert(std::count(v.begin(),v.end(),expected_0));     assert(std::count(v.begin(),v.end(),expected_1));     assert(std::count(v.begin(),v.end(),expected_2));     assert(std::count(v.begin(),v.end(),expected_3));     assert(std::count(v.begin(),v.end(),expected_4));     assert(std::count(v.begin(),v.end(),expected_5));     assert(std::count(v.begin(),v.end(),expected_6));     assert(std::count(v.begin(),v.end(),expected_7));   }   {     const std::vector<std::vector<int> > v = GetCombinations(std::vector<int>( { 1,2,3,4 } ) );     const std::vector<int> expected_0 = {};     const std::vector<int> expected_1 = {1};     const std::vector<int> expected_2 = {2};     const std::vector<int> expected_3 = {3};     const std::vector<int> expected_4 = {4};     const std::vector<int> expected_5 = {1,2};     const std::vector<int> expected_6 = {1,3};     const std::vector<int> expected_7 = {1,4};     const std::vector<int> expected_8 = {2,3};     const std::vector<int> expected_9 = {2,4};     const std::vector<int> expected_10 = {3,4};     const std::vector<int> expected_11 = {1,2,3};     const std::vector<int> expected_12 = {1,2,4};     const std::vector<int> expected_13 = {1,3,4};     const std::vector<int> expected_14 = {2,3,4};     const std::vector<int> expected_15 = {1,2,3,4};     assert(std::count(v.begin(),v.end(),expected_0));     assert(std::count(v.begin(),v.end(),expected_1));     assert(std::count(v.begin(),v.end(),expected_2));     assert(std::count(v.begin(),v.end(),expected_3));     assert(std::count(v.begin(),v.end(),expected_4));     assert(std::count(v.begin(),v.end(),expected_5));     assert(std::count(v.begin(),v.end(),expected_6));     assert(std::count(v.begin(),v.end(),expected_7));     assert(std::count(v.begin(),v.end(),expected_8));     assert(std::count(v.begin(),v.end(),expected_9));     assert(std::count(v.begin(),v.end(),expected_10));     assert(std::count(v.begin(),v.end(),expected_11));     assert(std::count(v.begin(),v.end(),expected_12));     assert(std::count(v.begin(),v.end(),expected_13));     assert(std::count(v.begin(),v.end(),expected_14));     assert(std::count(v.begin(),v.end(),expected_15));   } }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)