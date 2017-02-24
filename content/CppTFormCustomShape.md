

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [TForm custom shape](CppTFormCustomShape.htm)
==============================================================

 

[VCL](CppVcl.htm) [graphics](CppVclGraphics.htm) [code
snippet](CppVclCodeSnippets.htm) to use a custom TForm shape.

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` __fastcall TForm1::TForm1(TComponent* Owner) : TForm(Owner) {   HRGN h1 = CreateEllipticRgn(0,0,100,100);   HRGN h2 = CreateEllipticRgn(90,0,190,100);   HRGN h3 = CreateEllipticRgn(180,0,280,100);   CombineRgn(h1,h1,h2,RGN_OR);   CombineRgn(h1,h1,h3,RGN_OR);   SetWindowRgn(Handle,h1,true);   DeleteObject(h1);   DeleteObject(h2);   DeleteObject(h3); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)