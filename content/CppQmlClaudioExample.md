

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [QmlClaudioExample](CppQmlClaudioExample.htm)
==============================================================

 

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.htm)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.htm) 15.04 (vivid)

[IDE(s)](CppIde.htm):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.htm) 3.1.1

[Project type](CppQtProjectType.htm):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.htm)

[C++ standard](CppStandard.htm):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.9.2

[Libraries](CppLibrary.htm) used:

-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppQmlClaudioExample/CppQmlClaudioExample.pro
----------------------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` TEMPLATE = app  QT += qml quick  SOURCES += main.cpp  RESOURCES += qml.qrc  # Additional import path used to resolve QML modules in Qt Creator's code model QML_IMPORT_PATH =  # Default rules for deployment. include(deployment.pri)`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQmlClaudioExample/deployment.pri
-------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` android-no-sdk {     target.path = /data/user/qt     export(target.path)     INSTALLS += target } else:android {     x86 {         target.path = /libs/x86     } else: armeabi-v7a {         target.path = /libs/armeabi-v7a     } else {         target.path = /libs/armeabi     }     export(target.path)     INSTALLS += target } else:unix {     isEmpty(target.path) {         qnx {             target.path = /tmp/$${TARGET}/bin         } else {             target.path = /opt/$${TARGET}/bin         }         export(target.path)     }     INSTALLS += target }  export(INSTALLS)`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQmlClaudioExample/main.cpp
-------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <QGuiApplication> #include <QQmlApplicationEngine>  int main(int argc, char *argv[]) {     QGuiApplication app(argc, argv);      QQmlApplicationEngine engine;     engine.load(QUrl(QStringLiteral("qrc:///main.qml")));      return app.exec(); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQmlClaudioExample/timer.h
------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef TIMER_H #define TIMER_H  #include <QObject>  class Timer : public QObject {     Q_OBJECT public:     explicit Timer(QObject *parent = 0);  signals:  public slots:  };  #endif // TIMER_H`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQmlClaudioExample/timer.cpp
--------------------------------

 

  --------------------------------------------------------------------------------
  ` #include "timer.h"  Timer::Timer(QObject *parent) :     QObject(parent) { }`
  --------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)