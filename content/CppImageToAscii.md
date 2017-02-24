

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [ImageToAscii](CppImageToAscii.htm)
====================================================

 

[ASCII art](CppAsciiArt.htm) [code snippet](CppCodeSnippets.htm) to
convert a [VCL](CppVcl.htm) [TImage](CppTImage.htm) to a
[std::vector](CppVector.htm) of [std::string](CppString.htm).

 

The [tool](Tools.htm) [AsciiArter](ToolAsciiArter.htm) demonstrates
[ImageToAscii](CppImageToAscii.htm).

 

[ImageToAscii](CppImageToAscii.htm) uses the
[functions](CppFunction.htm)
[GetAsciiArtGradient](CppGetAsciiArtGradient.htm) and
[GetFractionGrey](CppGetFractionGrey.htm).

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `  #include <vector> #include <string> #include <algorithm> #include <cassert> #include <vcl.h>  //From http://www.richelbilderbeek.nl/CppImageToAscii.htm const std::vector<std::string> ImageToAscii(   const TImage * const image,   const int charWidth) //How many chars the ASCII image will be wide {   static const std::vector<char> chars(GetAsciiArtGradient());    //If the number of chars is below 5,   //the calculation would be more complicated due to a too trivial value of charWidth   assert(charWidth >= 5);    //Check the bitmap   assert(image!=0 && "Image must not be NULL");   assert(image->Picture->Bitmap != 0 && "Image bitmap must not be NULL");   assert(image->Picture->Bitmap->PixelFormat == pf24bit && "Image format must be 24-bit");     //Maxy is in proportion with the bitmap   const int maxy =     (static_cast<double>(charWidth)     / static_cast<double>(image->Picture->Bitmap->Width))     * static_cast<double>(image->Picture->Bitmap->Height);   assert(charWidth > 0);   assert(maxy > 0);   const double dX = static_cast<double>(image->Picture->Bitmap->Width)     / static_cast<double>(charWidth);   const double dY = static_cast<double>(image->Picture->Bitmap->Height)     / static_cast<double>(maxy);   assert(dX > 0.0);   assert(dY > 0.0);    std::vector<std::string> v;    for (int y=0; y!=maxy; ++y)   {     std::string myLine;     for (int x=0; x!=charWidth; ++x)     {       const int x1 = std::min(         static_cast<double>(x) * dX,         image->Picture->Bitmap->Width  - 1.0) + 0.5;       const int y1 = std::min(         static_cast<double>(y) * dY,         image->Picture->Bitmap->Height - 1.0) + 0.5;       const int x2 = std::min(         (static_cast<double>(x) * dX) + dX,         image->Picture->Bitmap->Width  - 1.0) + 0.5;       const int y2 = std::min(         (static_cast<double>(y) * dY) + dY,         image->Picture->Bitmap->Height - 1.0) + 0.5;       assert(x1 >= 0);       assert(x2 >= 0);       assert(y1 >= 0);       assert(y2 >= 0);       assert(x1 < image->Picture->Bitmap->Width);       assert(x2 < image->Picture->Bitmap->Width);       assert(y1 < image->Picture->Bitmap->Height);       assert(y2 < image->Picture->Bitmap->Height);        const double fGrey = std::min(         std::max(0.0, GetFractionGrey(image,x1,y1,x2,y2)),1.0);       assert(fGrey >= 0.0 && fGrey <= 1.0);       const double charIndex         = fGrey * static_cast<double>(chars.size() - 1);       assert(charIndex >= 0);       assert(charIndex < static_cast<int>(chars.size()));       const char thisChar = chars[charIndex];       myLine+=thisChar;     }     v.push_back(myLine);   }   return v; }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)