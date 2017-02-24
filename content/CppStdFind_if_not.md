

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [std::find\_if\_not](CppFind_if_not.htm)
=========================================================

 

[std::find\_if\_not](CppFind_if_not.htm) is a [C++11](Cpp11.htm)
[algorithm](CppAlgorithm.htm) to find an element in a
[container](CppContainer.htm) that does not satisfy a certain
[predicate](CppPredicate.htm).

 

-   [Download the Qt Creator project
    'CppFind\_if\_not' (zip)](CppFind_if_not.zip)

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <vector>  int main() {   const std::vector<int> v = { 1,3,5,7,9,10,11,13,15,17,19 };    assert(     *std::find_if_not(       v.begin(),v.end(),         [v](const int i)         {           return i%2; //An even number         }       )     == 10); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)