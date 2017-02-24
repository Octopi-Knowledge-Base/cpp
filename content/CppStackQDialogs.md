

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [StackQDialogs](CppStackQDialogs.htm)
======================================================

 

Technical facts
---------------

 

[Application type(s)](CppApplication.htm)

-   ![Desktop](PicDesktop.png) [Desktop
    application](CppDesktopApplication.htm)

[Operating system(s) or programming environment(s)](CppOs.htm)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.htm) 15.04 (vivid)

[IDE(s)](CppIde.htm):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.htm) 3.1.1

[Project type](CppQtProjectType.htm):

-   ![GUI](PicGui.png) [GUI application](CppGuiApplication.htm)

[C++ standard](CppStandard.htm):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.htm)

[Compiler(s)](CppCompiler.htm):

-   [G++](CppGpp.htm) 4.9.2

[Libraries](CppLibrary.htm) used:

-   ![Qt](PicQt.png) [Qt](CppQt.htm): version 5.4.1 (32 bit)
-   ![STL](PicStl.png) [STL](CppStl.htm): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppStackQDialogs/CppStackQDialogs.pro
--------------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #------------------------------------------------- # # Project created by QtCreator 2015-05-25T15:45:33 # #-------------------------------------------------  QT       += core gui  greaterThan(QT_MAJOR_VERSION, 4): QT += widgets  TARGET = CppStackQWidgets TEMPLATE = app   SOURCES += main.cpp\         dialog.cpp \     mydialog.cpp  HEADERS  += dialog.h \     mydialog.h  FORMS    += dialog.ui \     mydialog.ui`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStackQDialogs/dialog.h
---------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef DIALOG_H #define DIALOG_H  #include <QDialog>  namespace Ui { class Dialog; }  class Dialog : public QDialog {   Q_OBJECT  public:   explicit Dialog(QWidget *parent = 0);   ~Dialog();  private:   Ui::Dialog *ui; };  #endif // DIALOG_H`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStackQDialogs/dialog.cpp
-----------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "dialog.h"  #include <QGroupBox>  #include "mydialog.h" #include "ui_dialog.h"  Dialog::Dialog(QWidget *parent) :   QDialog(parent),   ui(new Ui::Dialog) {   ui->setupUi(this);    //Create a QGroupBox to stack the MyWidgets   QGroupBox * const b = new QGroupBox(this);    //A fresh QGroupBox does not have a layout yet   b->setLayout(new QVBoxLayout);    //Stack the MyWidgets   for (int i=0; i!=10; ++i)   {     b->layout()->addWidget(new MyDialog(this));   }    //Use setWidget   ui->scrollArea->setWidget(b); }  Dialog::~Dialog() {   delete ui; }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStackQDialogs/main.cpp
---------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "dialog.h" #include <QApplication>  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   Dialog w;   w.show();    return a.exec(); }`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStackQDialogs/mydialog.h
-----------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef MYDIALOG_H #define MYDIALOG_H  #include <QDialog>  namespace Ui { class MyDialog; }  class MyDialog : public QDialog {   Q_OBJECT  public:   explicit MyDialog(QWidget *parent = 0);   ~MyDialog();  private:   Ui::MyDialog *ui; };  #endif // MYDIALOG_H`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStackQDialogs/mydialog.cpp
-------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "mydialog.h" #include "ui_mydialog.h"  MyDialog::MyDialog(QWidget *parent) :   QDialog(parent),   ui(new Ui::MyDialog) {   ui->setupUi(this); }  MyDialog::~MyDialog() {   delete ui; }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)