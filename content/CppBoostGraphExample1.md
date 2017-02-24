

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [BoostGraphExample1](CppBoostGraphExample1.htm)
================================================================

 

![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[Boost.Graph example 1: four human names and their relationships +
plotting](CppBoostGraphExample1.htm) is a
[Boost.Graph](CppBoostGraph.htm) [example](CppExample.htm). It defines a
graph of person names and their relationships. Then the graph is written
to .dot file and plotted using KGraphViewer.

 

-   [View the graph of this example (png)](CppBoostGraphExample1.png)

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.htm): ./CppBoostGraphExample1/CppBoostGraphExample1.pro
------------------------------------------------------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++1y -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppBoostGraphExample1/main.cpp
--------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/graph/adjacency_list.hpp> #include <boost/graph/graphviz.hpp> #pragma GCC diagnostic pop  int main() {   //Define the type of graph:   //boost::adjacency_list is the 'Swiss army knife' graph   typedef boost::adjacency_list   <     //Store all out edges as a std::vector     boost::vecS,     //Store all vertices in a std::vector     boost::vecS,     //Relations are both ways (in this example)     //(note: but you can freely change it to boost::directedS)     boost::undirectedS,     //All vertices are person names of type std::string     boost::property<boost::vertex_name_t,std::string>,     //All edges are relation of type std::string     boost::property<boost::edge_name_t,std::string>   > Graph;    Graph  g;    const Graph::vertex_descriptor v1 = boost::add_vertex(std::string("Mr. A"),g);   const Graph::vertex_descriptor v2 = boost::add_vertex(std::string("Mrs. B"),g);   const Graph::vertex_descriptor v3 = boost::add_vertex(std::string("Dr. C"),g);   const Graph::vertex_descriptor v4 = boost::add_vertex(std::string("Prof. D"),g);   boost::add_edge(v1,v2,std::string("Married"),g);   boost::add_edge(v2,v3,std::string("Lovers"),g);   boost::add_edge(v3,v4,std::string("Collegues"),g);   boost::add_edge(v1,v4,std::string("Roommates"),g);    //Writing graph to file   {     std::ofstream f("test.dot");     //Problems:     //- All names are replaced by numbers     //- All relationships are omitted     boost::write_graphviz(f,g);     f.close();   }    //View the output directly using KGraphViewerer   std::system("kgraphviewer test.dot"); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)