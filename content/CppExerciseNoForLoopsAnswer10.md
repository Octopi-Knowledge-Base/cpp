

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [Answer of exercise \#9: No for-loops \#10](CppExerciseNoForLoopsAnswer10.htm)
===============================================================================================

 

This is the answer of [Exercise \#9: No
for-loops](CppExerciseNoForLoops.htm).

 

 

 

 

 

Question \#10: Widget::DoIt on [boost::shared\_ptr](CppShared_ptr.htm)&lt;Widget&gt;
------------------------------------------------------------------------------------

 

Replace the **[for](CppFor.htm)**-loop. You will need:

-   [std::for\_each](CppFor_each.htm)
-   [boost::mem\_fn](CppMem_fn.htm)

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector> #include <boost/shared_ptr.hpp>   struct Widget {   void DoIt() const { /* do it */ } };   void DoIt(const std::vector<boost::shared_ptr<Widget> >& v) {   const std::size_t sz = v.size();   for (std::size_t i=0; i!=sz; ++i)   {     v[i]->DoIt();   } }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Answer
------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <algorithm> #include <numeric> #include <vector> #include <boost/shared_ptr.hpp>  struct Widget {   void DoIt() const { /* do it */ } };  void DoIt(const std::vector<boost::shared_ptr<Widget> >& v) {   std::for_each(v.begin(),v.end(),boost::mem_fn(&Widget::DoIt)); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)