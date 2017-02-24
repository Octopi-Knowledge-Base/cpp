

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [std::find\_if](CppFind_if.htm)
================================================

 

[STL](CppStl.htm) [algorithm](CppAlgorithm.htm) for searching an
elements in a [container](CppContainer.htm), satisfying a certain
[predicate](CppPredicate.htm).

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <iterator> #include <vector>  int main() {   typedef std::vector<int>::const_iterator Iterator;    std::vector<int> v;   v.push_back(-2);   v.push_back(-1);   v.push_back( 0);   v.push_back( 1);   v.push_back( 2);    //Find the first element in v that has an integer value bigger then zero   const Iterator result     = std::find_if(v.begin(), v.end(),       std::bind2nd(std::greater<int>(), 0));    assert(result == v.end() && "A result is found");   assert(*result > 0 && "The result found is valid"); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)