

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [std::merge](CppMerge.htm)
===========================================

 

[std::merge](CppMerge.htm) is an [algorithm](CppAlgorithm.htm) that
merges two sorted [containers](CppContainer.htm) into a third sorted
[container](CppContainer.htm).

 

[std::merge](CppMerge.htm) is [defined](CppDefinition.htm) in the
[header file](CppHeaderFile.htm) [algorithm.h](CppAlgorithmH.htm).

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <iostream> #include <iterator> #include <vector>  int main() {   std::vector<int> v1;   v1.push_back(1);   v1.push_back(4);   v1.push_back(9);   v1.push_back(16);    std::vector<int> v2;   v2.push_back(1);   v2.push_back(1);   v2.push_back(2);   v2.push_back(3);   v2.push_back(5);   v2.push_back(8);   v2.push_back(13);    std::vector<int> v3;   //Merge v1 and v2 to v3   std::merge(     v1.begin(),v1.end(),     v2.begin(),v2.end(),     std::back_inserter(v3));   //Display v3   std::copy(     v3.begin(),v3.end(),     std::ostream_iterator<int>(std::cout,"\n")); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Screen output:

 

  ----------------------------
  ` 1 1 1 2 3 4 5 8 9 13 16`
  ----------------------------

 

 

 

 

 

External links
--------------

 

-   [SGI page about std::merge](http://www.sgi.com/tech/stl/merge.html)

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)