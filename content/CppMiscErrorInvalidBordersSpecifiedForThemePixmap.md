

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [Invalid borders specified for theme pixmap](CppMiscErrorInvalidBordersSpecifiedForThemePixmap.htm)
====================================================================================================================

 

[Misc error](CppMiscError.htm).

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` ** (ProjectVanDenBogaart:5134): WARNING **: Invalid borders specified for theme pixmap:         /usr/share/themes/Lubuntu-default/gtk-2.0/images/null.png, borders don't fit within the image  ** (ProjectVanDenBogaart:5134): WARNING **:     :         /usr/share/themes/Lubuntu-default/gtk-2.0/images/scrollbar_vertical.png, borders don't fit within the image`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Solution
--------

 

Originally, I used the rigorous following solution:

 

  -----------------------------------
  ` sudo apt-get install lubuntu-.`
  -----------------------------------

 

[Menachem](http://askubuntu.com/users/21794/menachem) pointed out at
[this askubuntu.com
thread](http://askubuntu.com/questions/225093/emacs-gives-warnings-in-lubuntu)
that the following might suffice:

 

  -----------------------------------------
  ` sudo apt-get install lubuntu-artwork`
  -----------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)