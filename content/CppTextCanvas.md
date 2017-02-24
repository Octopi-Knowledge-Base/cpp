

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [TextCanvas](CppTextCanvas.htm)
================================================

 

![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)![Windows](PicWindows.png)

 

[TextCanvas](CppTextCanvas.htm) is a [Canvas](CppCanvas.htm) to put text
on.

Technical facts
---------------

 

 

 

 

 

 

./CppTextCanvas/CppTextCanvas.pri
---------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppTextCanvas  SOURCES += \     ../../Classes/CppTextCanvas/textcanvas.cpp  HEADERS  += \     ../../Classes/CppTextCanvas/textcanvas.h  OTHER_FILES += \     ../../Classes/CppTextCanvas/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppTextCanvas/textcanvas.h
----------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef TEXTCANVAS_H #define TEXTCANVAS_H  #include <iosfwd> #include <string> #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/signals2.hpp> #include "canvas.h" #pragma GCC diagnostic pop  namespace ribi {  ///The TextCanvas is an ASCII art tool to write text ///The Canvas has a coordinat system of (0,0)-(width,height) ///similar to the possible character position on a screen. ///All texts written beyond the range of Canvas is not stored. ///Yet, if for example a text is written at an off-screen coordinat, ///the part that makes it to the Canvas is stored struct TextCanvas : public Canvas {   ///The number of characters the Canvas is heigh and wide   ///but also the maximum x and y coordinat. The minimum   ///x and y coordinats are 0 and 0   TextCanvas(     const int width  = 1,     const int height = 1,     const CanvasCoordinatSystem coordinatSystem = CanvasCoordinatSystem::screen   );   TextCanvas(const TextCanvas& rhs);   TextCanvas& operator=(const TextCanvas& rhs);    TextCanvas(     const std::vector<std::string>& canvas,     const CanvasCoordinatSystem coordinatSystem   );    ~TextCanvas() noexcept {}    ///Does the (x,y) coordinat exist?   bool CanGetChar(const int x, const int y) const noexcept { return IsInRange(x,y); }   bool CanPutChar(const int x, const int y) const noexcept { return IsInRange(x,y); }    ///Clears the canvas   void Clear() noexcept;    const std::vector<std::string>& GetCanvas() const noexcept { return m_canvas; }    CanvasCoordinatSystem GetCoordinatSystem() const noexcept { return m_coordinat_system; }    char GetChar(const int x, const int y) const noexcept;    ///Obtain the height of the canvas is characters   int GetHeight() const noexcept { return m_canvas.size(); }    static std::string GetVersion() noexcept;   static std::vector<std::string> GetVersionHistory() noexcept;    ///Obtain the width of the canvas is characters   int GetWidth() const noexcept { return (GetHeight()==0 ? 0 : m_canvas[0].size() ); }    ///Check if a coordinat is in the range of the Canvas   bool IsInRange(const int x, const int y) const noexcept;    void Load(const std::vector<std::string>& v) noexcept { m_canvas = v; }    ///Put a canvas on the canvas   void PutCanvas(     const int left, const int top,     const boost::shared_ptr<const TextCanvas>& canvas   ) noexcept;    ///Put a character on the Canvas   ///If the character is not in range, nothing happens   void PutChar(const int x, const int y, const char c) noexcept;    ///Put text to the Canvas   //   //  Canvas::DrawText(1,1,"Hello world") results in (I added dots for spaces, for clarity):   //   //  .............   //  .Hello world.   //  .............   //   void PutText(const int x, const int y, const std::string& text) noexcept;    ///Set the coordinat system used   void SetCoordinatSystem(const CanvasCoordinatSystem coordinatSystem) noexcept;    ///Convert to a single string, lines seperated with '\n'   std::string ToString() const noexcept;    ///Convert to a collection of strings   std::vector<std::string> ToStrings() const noexcept;    private:   ///The Canvas its internal data   std::vector<std::string> m_canvas;    ///The coordinat system used in displayal:   ///- screen: origin is at top-left of the screen   ///- graph: origin is at bottom-left of the screen   CanvasCoordinatSystem m_coordinat_system;    //From http://www.richelbilderbeek.nl/CppMinElement.htm   template <class Container>   static const typename Container::value_type::value_type MinElement(const Container& v);    //From http://www.richelbilderbeek.nl/CppMaxElement.htm   template <class Container>   static const typename Container::value_type::value_type MaxElement(const Container& v);    ///Plot a surface on screen   ///if as_screen_coordinat_system is true, the origin is in the top left   ///corner of the screen, else it is in the bottom left of the screen,   ///as is usual in graphs   //From http://www.richelbilderbeek.nl/CppPlotSurface.htm   static void PlotSurface(     std::ostream& os,     const std::vector<std::vector<double> >& v,     const bool use_normal_color_system,     const bool as_screen_coordinat_system);    #ifndef NDEBUG   static void Test() noexcept;   #endif    friend std::ostream& operator<<(std::ostream& os, const TextCanvas& canvas);  };  std::ostream& operator<<(std::ostream& os, const TextCanvas& canvas); bool operator==(const TextCanvas& lhs, const TextCanvas& rhs) noexcept; bool operator!=(const TextCanvas& lhs, const TextCanvas& rhs) noexcept;  } //~namespace ribi  #endif`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppTextCanvas/textcanvas.cpp
------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include "textcanvas.h"  #include <iostream> #include <cassert> #include <cmath> #include <algorithm> #include <functional> #include <iterator>  #include <boost/math/constants/constants.hpp>  #include "dotmatrixstring.h" #include "testtimer.h" #include "trace.h" #pragma GCC diagnostic pop  ribi::TextCanvas::TextCanvas(   const int width,   const int height,   const CanvasCoordinatSystem coordinatSystem)   : m_canvas(std::vector<std::string>(height,std::string(width,' '))),     m_coordinat_system(coordinatSystem) {   #ifndef NDEBUG   Test();   #endif   assert(width  > 0);   assert(height > 0); }  ribi::TextCanvas::TextCanvas(     const std::vector<std::string>& canvas,     const CanvasCoordinatSystem coordinatSystem ) : m_canvas(canvas),     m_coordinat_system(coordinatSystem) {   #ifndef NDEBUG   Test();   #endif }  ribi::TextCanvas::TextCanvas(const TextCanvas& rhs)   : m_canvas{rhs.m_canvas},     m_coordinat_system{rhs.m_coordinat_system} {  }  ribi::TextCanvas& ribi::TextCanvas::operator=(const TextCanvas& rhs) {   this->m_canvas = rhs.m_canvas;   this->m_coordinat_system = rhs.m_coordinat_system;   return *this; }  void ribi::TextCanvas::Clear() noexcept {   for (auto& row: m_canvas)   {     for (auto& cell:row)     {       cell = ' ';     }   }    #ifndef NDEBUG   for (const auto& row: m_canvas)   {     assert(std::count(row.begin(),row.end(),' ') == static_cast<int>(row.size()));   }   #endif   m_signal_changed(this); }  char ribi::TextCanvas::GetChar(const int x, const int y) const noexcept {   assert(IsInRange(x,y));   return m_canvas[y][x]; }  bool ribi::TextCanvas::IsInRange(const int x, const int y) const noexcept {   if (   x < 0       || y < 0       || y >= static_cast<int>(m_canvas.size())       || x >= static_cast<int>(m_canvas[y].size())      )     return false;   return true; }  std::string ribi::TextCanvas::GetVersion() noexcept {   return "1.0"; }  std::vector<std::string> ribi::TextCanvas::GetVersionHistory() noexcept {   return {     "2014-01-09: version 1.0: initial version"   }; }  void ribi::TextCanvas::PutCanvas(   const int left, const int top,   const boost::shared_ptr<const TextCanvas>& canvas ) noexcept {   const int height { canvas->GetHeight() };   const int width { canvas->GetWidth() };   for (int y=0; y!=height; ++y)   {     for (int x=0; x!=width; ++x)     {       PutChar(left + x, top + y,canvas->GetChar(x,y));     }   } }  void ribi::TextCanvas::PutChar(const int x, const int y, const char c) noexcept {   if(!IsInRange(x,y)) return;   if(m_canvas[y][x] != c)   {     m_canvas[y][x] = c;     m_signal_changed(this);   } }  void ribi::TextCanvas::PutText(const int x, const int y, const std::string& text) noexcept {   int i=0;   for (const auto& c: text)   {     const int x_here = x + i;     const int y_here = y;     if (IsInRange(x_here,y_here))     {       PutChar(x_here,y_here,c);     }     ++i;   } }  void ribi::TextCanvas::SetCoordinatSystem(const CanvasCoordinatSystem coordinatSystem) noexcept {   if (this->m_coordinat_system != coordinatSystem)   {     this->m_coordinat_system = coordinatSystem;     this->m_signal_changed(this);   } }  #ifndef NDEBUG void ribi::TextCanvas::Test() noexcept {   {     static bool is_tested{false};     if (is_tested) return;     is_tested = true;   }   const TestTimer test_timer(__func__,__FILE__,1.0);   //Drawing text   {     const int maxx = 90;     const int maxy = 18;     const boost::shared_ptr<TextCanvas> canvas(new TextCanvas(maxx,maxy));     std::stringstream s_before;     s_before << (*canvas);     const std::string str_before {s_before.str() };     assert(static_cast<int>(str_before.size()) - maxy == maxx * maxy); //-maxy, as newlines are added     assert(std::count(str_before.begin(),str_before.end(),' ') == maxx * maxy); //Only spaces      canvas->PutText(1,1,"Hello world");      std::stringstream s_after;     s_after << (*canvas);     const std::string str_after {s_after.str() };     assert(std::count(str_after.begin(),str_after.end(),' ') != maxx * maxy); //Line trly drawn   }   //Is a text that starts before the canvas partially accepted?   {     const int maxx = 3;     const int maxy = 4;     const boost::shared_ptr<TextCanvas> canvas(new TextCanvas(maxx,maxy));     std::stringstream s_before;     s_before << (*canvas);     const std::string str_before {s_before.str() };     assert(static_cast<int>(str_before.size()) - maxy == maxx * maxy); //-maxy, as newlines are added     assert(std::count(str_before.begin(),str_before.end(),' ') == maxx * maxy); //Only spaces      canvas->PutText(-5,1,"Hello world");      std::stringstream s_after;     s_after << (*canvas);     const std::string str_after {s_after.str() };     assert(std::count(str_after.begin(),str_after.end(),' ') != maxx * maxy); //Line truely drawn   }   //Copy constructor   {     const TextCanvas a(3,4);     const TextCanvas b(a);     assert(a==b);   }   //Assignment operator   {     const TextCanvas a(3,4);     TextCanvas b(4,5);     assert(a!=b);     b = a;     assert(a==b);   } } #endif  std::string ribi::TextCanvas::ToString() const noexcept {   const std::vector<std::string> v { ToStrings() };   std::string s;   for (const auto& t: v)   {     s += t;     s += '\n';   }   if (!s.empty())   {     //Remove the trailing '\n'     s.pop_back();   }   return s; }   std::vector<std::string> ribi::TextCanvas::ToStrings() const noexcept {   if (m_coordinat_system == CanvasCoordinatSystem::screen)   {     return m_canvas;   }   else   {     std::vector<std::string> v(m_canvas);     std::reverse(std::begin(v),std::end(v));     return v;   } }  std::ostream& ribi::operator<<(std::ostream& os, const TextCanvas& canvas) {   const auto v = canvas.ToStrings();   std::copy(v.begin(),v.end(),     std::ostream_iterator<std::string>(os,"\n")   );   return os; }  bool ribi::operator==(const TextCanvas& lhs, const TextCanvas& rhs) noexcept {   return lhs.ToString() == rhs.ToString(); }  bool ribi::operator!=(const TextCanvas& lhs, const TextCanvas& rhs) noexcept {   return !(lhs == rhs); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)