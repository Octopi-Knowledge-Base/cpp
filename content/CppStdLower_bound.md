

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [std::lower\_bound](CppLower_bound.htm)
========================================================

 

[std::lower\_bound](CppLower_bound.htm) is an [STL](CppStl.htm)
[algorithm](CppAlgorithm.htm) to find an element in a
[container](CppContainer.htm) smaller than a certain value.

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <vector>  int main() {   std::vector<int> v;   v.push_back(1);   v.push_back(2);   v.push_back(3);    //Lower bound will point to first element not smaller than 2   assert(*std::lower_bound(v.begin(),v.end(),2)==2);    //Upper bound will point to first element larger than 2   assert(*std::upper_bound(v.begin(),v.end(),2)==3); } `
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)