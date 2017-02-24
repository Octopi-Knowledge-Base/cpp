

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [Undefined reference to 'QGraphicsItemPrivate::height() const'](CppLinkErrorUndefinedReferenceToQGraphicsItemPrivateHeight.htm)
================================================================================================================================================

 

[link error](CppLinkError.htm).

 

 

 

 

 

Full error message
------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` /home/richel/qtsdk-2010.04/lib/libQtSvg.so.4:: error: undefined reference to 'QGraphicsItemPrivate::height() const' /home/richel/qtsdk-2010.04/lib/libQtSvg.so.4:: error: undefined reference to 'QListData::detach(int)' /home/richel/qtsdk-2010.04/lib/libQtSvg.so.4:: error: undefined reference to 'QGraphicsItemPrivate::setWidth(double)' /home/richel/qtsdk-2010.04/lib/libQtSvg.so.4:: error: undefined reference to 'QGraphicsItemPrivate::width() const' /home/richel/qtsdk-2010.04/lib/libQtSvg.so.4:: error: undefined reference to 'QGraphicsItemPrivate::setHeight(double)' /home/richel/qtsdk-2010.04/lib/libQtSvg.so.4:: error: undefined reference to 'QGraphicsItemPrivate::resetHeight()' /home/richel/qtsdk-2010.04/lib/libQtSvg.so.4:: error: undefined reference to 'QGraphicsItemPrivate::resetWidth()' /home/richel/qtsdk-2010.04/lib/libQtSvg.so.4:: error: undefined reference to 'QListData::detach_grow(int*, int)' :: error: collect2: ld returned 1 exit status`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Cause
-----

 

Operating system: [Ubuntu](http://www.ubuntu.com) 10.04 LTS Lucid Lynx

[IDE](CppIde.htm): [Qt Creator](CppQtCreator.htm) 2.0.0

[Project type](CppQtProjectType.htm): Console Application

[Compiler](CppCompiler.htm): [G++](CppGpp.htm) 4.4.1

[Libraries](CppLibrary.htm) used:

-   [Qt](CppQt.htm): version 4.7.0 (32 bit)

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm)
---------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #------------------------------------------------- # # Project created by QtCreator 2010-07-21T19:21:43 # #------------------------------------------------- QT       += core gui TARGET = CppQwtExample1 TEMPLATE = app SOURCES += main.cpp LIBS += -L/usr/local/lib -lqwt-qt4`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Source code
-----------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <QApplication>  #include <qwt-qt4/qwt_plot.h>  int main(int argc, char **argv) {   QApplication a(argc, argv);   QwtPlot plot;   plot.show();   return a.exec(); }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Solution
--------

 

You will additionaly need to link to QtSvg.

 

Add the following line to the [Qt Creator](CppQtCreator.htm) [project
file](CppQtProjectFile.htm):

 

  -------------------------------------
  ` LIBS += -L/usr/local/lib -lQtSvg`
  -------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)