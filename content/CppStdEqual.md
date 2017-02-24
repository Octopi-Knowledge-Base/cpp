

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [std::equal](CppEqual.htm)
===========================================

 

[std::equal](CppEqual.htm) is an [STL](CppStl.htm)
[algorithm](CppAlgorithm.htm) to compare two ranges for equality.

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <vector>  int main() {   std::vector<int> v1;   v1.push_back( std::rand() );   v1.push_back( std::rand() );   v1.push_back( std::rand() );     std::vector<int> v2(v1);    assert(std::equal(v1.begin(),v1.end(),v2.begin()));    v2.push_back( std::rand() );     assert( std::equal(v1.begin(),v1.end(),v2.begin()));   assert(!std::equal(v2.begin(),v2.end(),v1.begin())); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)