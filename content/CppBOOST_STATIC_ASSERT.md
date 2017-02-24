

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [BOOST\_STATIC\_ASSERT](CppBOOST_STATIC_ASSERT.htm)
====================================================================

 

[BOOST\_STATIC\_ASSERT](CppBOOST_STATIC_ASSERT.htm) is a
[Boost](CppBoost.htm) [macro](CppMacro.htm)[]() to test assertions (that
can be made at [compile time](CppCompileTime.htm)) at [compile
time](CppCompileTime.htm).

 

  ----------------------------------------------------------------------------------------------------------------------------------------
  ` #include <boost/static_assert.hpp>  int main() {   BOOST_STATIC_ASSERT(16 * 16 == 256);   BOOST_STATIC_ASSERT(sizeof(char) == 1); }`
  ----------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

![C++11](PicCpp11.png) Note for users of the [C++11](Cpp11.htm) [standard](CppStandard.htm)
-------------------------------------------------------------------------------------------

 

The [C++11](Cpp11.htm) [standard](CppStandard.htm) has the
[keyword](CppKeyword.htm) [static\_assert](CppStatic_assert.htm) serving
the same function.

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)