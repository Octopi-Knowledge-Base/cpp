

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [Answer of exercise \#9: No for-loops \#31](CppExerciseNoForLoopsAnswer31.htm)
===============================================================================================

 

This is the answer of [Exercise \#9: No
for-loops](CppExerciseNoForLoops.htm).

 

 

 

 

 

Question \#31: Find an ID in a [std::vector](CppVector.htm)&lt;**[const](CppConst.htm)** Person\*&gt;
-----------------------------------------------------------------------------------------------------

 

Replace the **[for](CppFor.htm)**-loop. You will need:

-   [boost::bind](CppBind.htm)

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <vector>  struct Id {   Id(const int id) : m_id(id) { }   int Get() const { return m_id; }   private:   int m_id; };  struct Person {   Person(const int id) : m_id(new Id(id)) {}   const Id * GetId() const { return m_id.get(); }   private:   boost::scoped_ptr<Id> m_id; };  bool IsIdTaken(const std::vector<const Person*>& v, const int id) {   const int sz = static_cast<int>(v.size());   for (int i=0; i!=sz; ++i)   {     if (v[i]->GetId()->Get() == id) return true;   }   return false; }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

![Boost](PicBoost.png) Answer using [Boost](CppBoost.htm).Bind
--------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <vector> #include <boost/bind.hpp> #include <boost/lambda/bind.hpp> #include <boost/scoped_ptr.hpp>  struct Id {   Id(const int id) : m_id(id) { }   int Get() const { return m_id; }   private:   int m_id; };  struct Person {   Person(const int id) : m_id(new Id(id)) {}   const Id * GetId() const { return m_id.get(); }   private:   boost::scoped_ptr<Id> m_id; };  bool IsIdTaken(const std::vector<const Person*>& v, const int id) {   return std::find_if(     v.begin(),v.end(),       boost::bind(&Id::Get,         boost::bind(&Person::GetId,boost::lambda::_1)         ) == id     ) != v.end(); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

![FAIL](PicRed.png)![Cpp11](PicCpp11.png) Failed attempt using [C++11](Cpp11.htm)
---------------------------------------------------------------------------------

 

Sadly, this does not work and I do not understand why yet...

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` bool IsIdTaken(const std::vector<const Person*>& v, const int id) {   return std::find_if(     v.begin(),v.end(),       [id](const Person * person) { person->GetId()->Get() == id; }     ) != v.end(); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)