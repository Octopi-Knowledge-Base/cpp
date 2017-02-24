

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [std::stable\_sort](CppStable_sort.htm)
========================================================

 

[std::stable\_sort](CppStable_sort.htm) is an [STL](CppStl.htm)
[sorting](CppSort.htm) [algorithm](CppAlgorithm.htm). It differs from
[std::sort](CppSort.htm) in that it preserves the order in equivalent
elemenst (where [std::sort](CppSort.htm) might change this order).

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <cassert> #include <vector>  struct MyClass {   MyClass(const int id, const int something)     : m_id(id), m_something(something) {}    int m_id;   int m_something; };  bool operator<(const MyClass& lhs, const MyClass& rhs) {   //Note: m_something is not tested for   return lhs.m_id < rhs.m_id; }  int main() {   std::vector<MyClass> v;   v.push_back(MyClass(2,2));   v.push_back(MyClass(1,2)); //These three instances   v.push_back(MyClass(1,1)); //will remain in the same   v.push_back(MyClass(1,0)); //order after std::stable_sort   v.push_back(MyClass(0,0));    std::stable_sort(v.begin(),v.end());   assert(v[0].m_id == 0 && v[0].m_something == 0);   assert(v[1].m_id == 1 && v[1].m_something == 2);   assert(v[2].m_id == 1 && v[2].m_something == 1);   assert(v[3].m_id == 1 && v[3].m_something == 0);   assert(v[4].m_id == 2 && v[4].m_something == 2); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

External links
--------------

 

-   [SGI page about
    std::stable\_sort](http://www.sgi.com/tech/stl/stable_sort.html)

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)