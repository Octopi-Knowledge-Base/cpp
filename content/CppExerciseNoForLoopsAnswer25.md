

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [Answer of exercise \#9: No for-loops \#25](CppExerciseNoForLoopsAnswer25.htm)
===============================================================================================

 

This is the answer of [Exercise \#9: No
for-loops](CppExerciseNoForLoops.htm).

 

 

 

 

 

Question \#25: HasMale on std::vector&lt;Person\*&gt;
-----------------------------------------------------

 

Replace the **[for](CppFor.htm)**-loop. You will need:

-   [boost::bind](CppBind.htm)

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector> #include <boost/numeric/conversion/cast.hpp>  struct Person {   Person(const bool is_male) : m_is_male(is_male) {}   bool IsMale() const { return m_is_male; }   const bool m_is_male; };  bool HasMale(const std::vector<const Person *>& v) {   const int size = boost::numeric_cast<int>(v.size());   for (int i=0; i!=size; ++i)   {     if (v[i]->IsMale()) return true;   }   return false; }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

![Boost](PicBoost.png) Answer using [Boost](CppBoost.htm).Bind
--------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <vector> #include <boost/bind.hpp> #include <boost/numeric/conversion/cast.hpp>  struct Person {   Person(const bool is_male) : m_is_male(is_male) {}   bool IsMale() const { return m_is_male; }   const bool m_is_male; };  bool HasMale(const std::vector<const Person *>& v) {   return std::find_if(     v.begin(),v.end(),     boost::mem_fn(&Person::IsMale)     ) != v.end(); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)