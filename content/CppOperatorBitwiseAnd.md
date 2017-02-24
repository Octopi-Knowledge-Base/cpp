

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [operator&](CppOperatorBitwiseAnd.htm)
=======================================================

 

[operator&](CppOperatorBitwiseAnd.htm) (pronounced as 'bitwise and
[operator](CppOperator.htm)') is an [operator](CppOperator.htm) to
perform a bitwise and.

 

  -------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert>  int main() {   int x = 3;     //0011   int y = 5;     //0101   int z = x & y; //0001   assert(z==1); }`
  -------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Example: bitflags
-----------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  void ShowFlags(const int i) {   if (i & 1) std::cout << "1\n";   if (i & 2) std::cout << "2\n";   if (i & 4) std::cout << "4\n";   if (i & 8) std::cout << "8\n"; }  int main() {   ShowFlags(15); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)