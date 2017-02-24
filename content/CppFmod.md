

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [Fmod](CppFmod.htm)
====================================

 

[Fmod](CppFmod.htm) is a [math](CppMath.htm) [function](CppFunction.htm)
to perform a [modulus operation](CppOperatorModulus.htm) on
[doubles](CppDouble.htm).

 

[std::modf](CppModf.htm) has a different purpose as [Fmod](CppFmod.htm):
[std::modf](CppModf.htm) splits a [double](CppDouble.htm) into its
[integer](CppInt.htm) and a fractional part, for example it splits 12.34
into 12 and 0.34

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert>   double Fmod(const double x, const double mod) {   assert(mod != 0.0); //Cannot divide by zero   return x - (mod * static_cast<int>(x / mod)); }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)