

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [QtRubiksClockWidget](CppQtRubiksClockWidget.htm)
==================================================================

 

![Qt](PicQt.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[QtRubiksClockWidget](CppQtRubiksClockWidget.htm) is a [Qt](CppQt.htm)
[class](CppClass.htm) for displaying a Rubik's Clock.

Technical facts
---------------

 

 

 

 

 

 

./CppQtRubiksClockWidget/CppQtRubiksClockWidget.pri
---------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppQtRubiksClockWidget  SOURCES += \     ../../Classes/CppQtRubiksClockWidget/qtrubiksclockwidget.cpp  HEADERS  += \     ../../Classes/CppQtRubiksClockWidget/qtrubiksclockwidget.h  OTHER_FILES += \     ../../Classes/CppQtRubiksClockWidget/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtRubiksClockWidget/qtrubiksclockwidget.h
----------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* QtRubiksClockWidget, Wt widget for displaying the RubiksClock class Copyright (C) 2011-2015 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program. If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppQtRubiksClockWidget.htm //--------------------------------------------------------------------------- #ifndef QTRUBIKSCLOCKWIDGET_H #define QTRUBIKSCLOCKWIDGET_H  #include <string> #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/signals2.hpp>  #include <QWidget>  #include "rubiksclock.h"       //Required by MOC #include "rubiksclockfwd.h" #include "rubiksclockwidget.h" //Required by MOC #pragma GCC diagnostic pop  namespace Wt { struct WMouseEventEvent; } struct QPainter;  namespace ribi { namespace ruco {  ///QtRubiksClockWidget displays a RubiksClock class QtRubiksClockWidget : public QWidget {   Q_OBJECT  public:   ///A QtRubiksClockWidget is created by its toggle state and its color   QtRubiksClockWidget(     const bool toggled = false,     const unsigned char red = 255,     const unsigned char green = 255,     const unsigned char blue = 255);    ///Obtain a read-only pointer to the RubiksClockWidget   const ClockWidget * GetWidget() const { return m_widget.get(); }    ///Obtain a read-and-write pointer to the RubiksClockWidget   ClockWidget * GetWidget() { return m_widget.get(); }    ///Obtain the QtRubiksClockWidget its version   static std::string GetVersion() noexcept;    ///Obtain the QtRubiksClockWidget its version history   static std::vector<std::string> GetVersionHistory() noexcept;    ///\brief   ///Draw the RubiksClock   ///   ///Because a Rubik's Clock has two sides, the parameter   ///front_size determines whether to draw the front side or the back side   static void DrawRubiksClock(     QPainter& painter,     const int x, const int y,     const int width, const int height,     const Clock * const clock,     const bool front_size);    ///Draw the RubiksClock   static void DrawRubiksClock(     QPainter& painter,     const ClockWidget * const widget);    protected:   ///Paint the QtRubiksClockWidget   void paintEvent(QPaintEvent *);   //void paintEvent(Wt::WPaintDevice *paintDevice);   void mousePressEvent(QMouseEvent *);    private:   ///The RubiksClockWidget   boost::scoped_ptr<ClockWidget> m_widget;    ///Do not let this be called by the client   void resize(const int width, const int height);    ///Repaint the QtRubiksClockWidget   void DoRepaint();    ///Respond to the widget resizing   void OnResize(); };  } //~namespace ruco } //~namespace ribi  #endif // QTRUBIKSCLOCKWIDGET_H`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtRubiksClockWidget/qtrubiksclockwidget.cpp
------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* QtRubiksClockWidget, Wt widget for displaying the RubiksClock class Copyright (C) 2011-2015 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program. If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppQtRubiksClockWidget.htm //--------------------------------------------------------------------------- #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include "qtrubiksclockwidget.h"  #include <cassert> #include <iostream> #include <boost/bind.hpp> #include <boost/numeric/conversion/cast.hpp>  #include <QMouseEvent> #include <QPainter>  #include "dial.h" #include "qtdialwidget.h" #include "qttogglebuttonwidget.h" #include "rubiksclock.h" #include "rubiksclockdial.h" #include "rubiksclockdialwidget.h" #include "rubiksclockpegs.h" #include "rubiksclocktimes.h" #include "rubiksclockwidget.h" #include "togglebutton.h" #include "togglebuttonwidget.h" #include "trace.h"  #pragma GCC diagnostic pop  ribi::ruco::QtRubiksClockWidget::QtRubiksClockWidget(   const bool toggled,   const unsigned char red,   const unsigned char green,   const unsigned char blue)   : m_widget(new ClockWidget(toggled,red,green,blue)) {   assert(m_widget);    m_widget->m_signal_widget_flipped.connect(     boost::bind(       &ribi::ruco::QtRubiksClockWidget::DoRepaint,       this));    m_widget->GetRubiksClock()->m_signal_clock_changed.connect(     boost::bind(       &ribi::ruco::QtRubiksClockWidget::DoRepaint,       this));    m_widget->m_signal_geometry_changed.connect(     boost::bind(       &ribi::ruco::QtRubiksClockWidget::OnResize,       this));    m_widget->SetGeometry(0,0,200,200); }  void ribi::ruco::QtRubiksClockWidget::DoRepaint() {   this->update(); }  void ribi::ruco::QtRubiksClockWidget::DrawRubiksClock(   QPainter& painter,   const int left, const int top,   const int width, const int height,   const Clock * const clock,   const bool front_side) {   //Draw main clock ring   {     QPen pen = painter.pen();     pen.setColor(Qt::black);     painter.setPen(pen);   }   {     painter.setBrush(       QBrush(         QColor(           front_side ? 127 : 96,           front_side ? 127 : 96,           196         )       )     );   }   painter.drawEllipse(     static_cast<double>(left),     static_cast<double>(top),     static_cast<double>(width),     static_cast<double>(height)   );      //Draw the clocks and pegs   {     for (int y=0; y!=3; ++y)     {       for (int x=0; x!=3; ++x)       {         const boost::shared_ptr<ClockDialWidget> w           = (front_side ? clock->GetFrontTimes() : clock->GetBackTimes())->times[x][y];         QtDialWidget::DrawDial(           painter,           w->GetLeft(),           w->GetTop(),           w->GetWidth(),           w->GetHeight(),           w->GetRubiksClockDial()->GetDial()         );       }     }     //Draw the pegs     for (int y=0; y!=2; ++y)     {       for (int x=0; x!=2; ++x)       {         QtToggleButtonWidget::DrawToggleButton(           painter,           (front_side             ? clock->GetFrontPegs()             : clock->GetBackPegs())->m_pegs[x][y]         );       }     }   } }  void ribi::ruco::QtRubiksClockWidget::DrawRubiksClock(   QPainter& painter,   const ClockWidget * const widget) {   DrawRubiksClock(     painter,     widget->GetLeft(),     widget->GetTop(),     widget->GetWidth(),     widget->GetHeight(),     widget->GetRubiksClock(),     widget->GetDisplayFront()); }  std::string ribi::ruco::QtRubiksClockWidget::GetVersion() noexcept {   return "1.2"; }  std::vector<std::string> ribi::ruco::QtRubiksClockWidget::GetVersionHistory() noexcept {   return {     "2012-12-22: version 1.0: initial version"     "2014-01-23: version 1.1: put in namespace ruco",     "2014-03-28: version 1.2: replaced Rect by Boost.Geometry its box class"   }; }  void ribi::ruco::QtRubiksClockWidget::mousePressEvent(QMouseEvent * e) {   const int x = e->x();   const int y = e->y();    const bool is_left_button = e->button() == Qt::LeftButton;   m_widget->Click(x,y,is_left_button); }  void ribi::ruco::QtRubiksClockWidget::OnResize() {   resize(m_widget->GetWidth(),m_widget->GetHeight()); }  void ribi::ruco::QtRubiksClockWidget::paintEvent(QPaintEvent *) {   QPainter painter(this);   DrawRubiksClock(painter,m_widget.get()); }  void ribi::ruco::QtRubiksClockWidget::resize(const int width, const int height) {   QWidget::resize(width,height); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)