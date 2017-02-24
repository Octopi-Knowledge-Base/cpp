

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [BoostGraphExample4](CppBoostGraphExample4.htm)
================================================================

 

![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[Boost.Graph example 4: four human names and their relationships
displayed in Qt](CppBoostGraphExample4.htm) is a
[Boost.Graph](CppBoostGraph.htm) [example](CppExample.htm). It defines a
graph of person names and their relationships. Then the graph is written
to .dot file and plotted using KGraphViewer.

 

-   [View the graph of this example (png)](CppBoostGraphExample4.png)

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppBoostGraphExample4/CppBoostGraphExample4.pro
------------------------------------------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../DesktopApplication.pri) #Or use the code below # QT       += core gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # # win32 { #   greaterThan(QT_MAJOR_VERSION, 4): QT += svg # } # # TEMPLATE = app # # CONFIG(debug, debug|release) { #   message(Debug mode) # } # # CONFIG(release, debug|release) { #   message(Release mode) #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # # QMAKE_CXXFLAGS += -std=c++1y -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  include(../../Libraries/Poppler.pri) #Or use the code below # unix { #   LIBS += -L/usr/local/bin -lpoppler-qt4 # }  QT       += core gui xml SOURCES += main.cpp \         dialogmain.cpp HEADERS  += dialogmain.h FORMS    += dialogmain.ui RESOURCES += resources.qrc`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostGraphExample4/dialogmain.h
------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `  #ifndef DIALOGMAIN_H #define DIALOGMAIN_H  #include <QDialog>  namespace Ui {   class DialogMain; }  class DialogMain : public QDialog {   Q_OBJECT  public:   explicit DialogMain(QWidget *parent = 0);   ~DialogMain();  private:   Ui::DialogMain *ui; };  #endif // DIALOGMAIN_H`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostGraphExample4/dialogmain.cpp
--------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "dialogmain.h"  #include <cstdio>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/graph/adjacency_list.hpp> #include <boost/graph/graphviz.hpp>  #include <poppler/qt4/poppler-qt4.h>  #include "ui_dialogmain.h" #pragma GCC diagnostic pop DialogMain::DialogMain(QWidget *parent) :     QDialog(parent, Qt::Window),     ui(new Ui::DialogMain) {   ui->setupUi(this);    //Write a graph to file   //Define the type of graph:   //boost::adjacency_list is the 'Swiss army knife' graph   typedef boost::adjacency_list   <     //Store all edges as a std::vector     boost::vecS,     //Store all vertices in a std::vector     boost::vecS,     //Relations are both ways (in this example)     //(note: but you can freely change it to boost::directedS)     boost::undirectedS,     //All vertices are person names of type std::string     boost::property<boost::vertex_name_t,std::string>,     //All edges are weights equal to the encounter frequencies     boost::property<boost::edge_weight_t,double>,     //Graph itself has a std::string name     boost::property<boost::graph_name_t,std::string>   > Graph;    Graph  g;    //All vertex names   //Note: cannot use spaces   std::vector<std::string> names;   names.push_back("Mr_A");   names.push_back("Mrs_B");   names.push_back("Dr_C");   names.push_back("Prof_D");    const Graph::vertex_descriptor v0 = boost::add_vertex(names[0],g);   const Graph::vertex_descriptor v1 = boost::add_vertex(names[1],g);   const Graph::vertex_descriptor v2 = boost::add_vertex(names[2],g);   const Graph::vertex_descriptor v3 = boost::add_vertex(names[3],g);    std::vector<double> frequencies;   frequencies.push_back(0.9);   frequencies.push_back(0.5);   frequencies.push_back(0.6);   frequencies.push_back(0.1);    boost::add_edge(v0,v1,frequencies[0],g);   boost::add_edge(v1,v2,frequencies[1],g);   boost::add_edge(v2,v3,frequencies[2],g);   boost::add_edge(v0,v3,frequencies[3],g);    //Writing graph to file   {     std::ofstream f("test.dot");      boost::dynamic_properties p;     p.property("label", boost::get(boost::edge_weight, g));     p.property("weight", boost::get(boost::edge_weight, g));     p.property("node_id", boost::get(boost::vertex_name, g));     boost::write_graphviz(f,g,p);     f.close();   }   //Convert test.dot file to test.pdf   std::system("dot2tex test.dot > test.tex");   std::system("texi2pdf test.tex");    //Load test.pdf in QLabel   Poppler::Document *doc = Poppler::Document::load("test.pdf");   const int current_page = 0;   const double scale = 1.0;    QImage image = doc->page(current_page)->renderToImage(                             scale * physicalDpiX(),                             scale * physicalDpiY());    ui->label->setPixmap(QPixmap::fromImage(image)); }  DialogMain::~DialogMain() {   delete ui; }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostGraphExample4/main.cpp
--------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <QApplication> #include "dialogmain.h" #pragma GCC diagnostic pop  int main(int argc, char *argv[]) {   QApplication a(argc, argv);   DialogMain w;   w.show();   return a.exec(); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)