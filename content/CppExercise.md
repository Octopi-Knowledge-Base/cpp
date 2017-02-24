

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [Exercise](CppExercise.htm)
============================================

 

![STL](PicStl.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

On this page you can find some exercises about correct programming,
inspired by [Herb Sutter](CppHerbSutter.htm)'s 'Guru Of The Week' pages.

 

These [exercises](CppExercise.htm) are suitable for experienced
beginners, that want to learn to think in the C++ way. As a side-result
they will learn more advanced concepts in a playful way. I try to work
on the same difficulty scale as [Herb Sutter](CppHerbSutter.htm).

 

-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#0: A correct
    Divide function](CppExerciseDivide.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#1: A foolproof
    function](CppExerciseFoolproofFunction.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#2: Correct
    function declarations](CppExerciseCorrectFunctionDeclarations.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#3: Don't give
    away your internals](CppExerciseDontGiveAwayYourInternals.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#4: Reading
    from a std::vector safely](CppExerciseReadingFromAvectorSafely.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#5: The many
    types of const](CppExerciseTheManyTypesOfConst.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#6: refactoring
    quadratic solver](CppExerciseRefactoringQuadraticSolver.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#7: add
    one](CppExerciseAddOne.htm)
-   ![C++98](PicCpp98.png)![C++ Builder](PicCppBuilder.png) [Exercise
    \#8: library trouble](CppExerciseLibraryTrouble.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#9: no
    for-loops](CppExerciseNoForLoops.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#10: Obtaining
    a read-only (smart?) pointer](CppExerciseReadonlyPointer.htm)
-   ![C++98](PicCpp98.png)![ ](PicSpacer.png) [Exercise \#11: Obtaining
    a std::vector of read-only (smart?)
    pointers](CppExerciseReadonlyVectorOfPointers.htm)
-   ![C++98](PicCpp98.png)![Qt](PicQt.png) [Exercise \#12: Qt hide and
    show \#1: intro](CppExerciseQtHideAndShow1.htm)
-   ![C++98](PicCpp98.png)![Qt](PicQt.png) [Exercise \#13: Qt hide and
    show \#2: the real problem](CppExerciseQtHideAndShow2.htm)
-   ![C++98](PicCpp98.png)![Qt](PicQt.png) [Exercise \#14: Qt hide and
    show \#3: refactoring](CppExerciseQtHideAndShow3.htm)

 

 

 

 

 

External links
--------------

 

1.  [Herb Sutter's Guru Of The Week archive](http://www.gotw.ca/gotw/)

Additionally, [Exercise](CppExercise.htm) is a [class](CppClass.htm) for
an exercise.

Technical facts
---------------

 

 

 

 

 

 

./CppExercise/CppExercise.pri
-----------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppExercise  SOURCES += \     ../../Classes/CppExercise/exercise.cpp  HEADERS  += \     ../../Classes/CppExercise/exercise.h  OTHER_FILES += \     ../../Classes/CppExercise/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppExercise/exercise.h
------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* Exercise, a collection of Questions Copyright (C) 2011-2015 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program.If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppExercise.htm //--------------------------------------------------------------------------- #ifndef EXERCISE_H #define EXERCISE_H  #include <string> #include <vector>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #include <boost/shared_ptr.hpp> #pragma GCC diagnostic pop  namespace ribi {  ///A Exercise is a collection of questions struct Exercise {   ///Construct a Exercise from file   ///The file needs to contain at least one question   ///Throws std::logic_error if file does not exist   ///Throws std::runtime_error if file does not contain a single question   explicit Exercise(const std::string& filename);    ///Read the current question   std::string GetCurrentQuestion() const noexcept;    ///Get the number of questions, will be at least one   int GetNumberOfQuestions() const noexcept;    ///Obtain this class its version   static std::string GetVersion() noexcept;    ///Obtain this class its version history   static std::vector<std::string> GetVersionHistory() noexcept;    ///Go to the next question   void Next() noexcept;    private:   ~Exercise() noexcept {}   friend void boost::checked_delete<>(Exercise *);   friend void boost::checked_delete<>(const Exercise *);    ///An iterator pointing to the current question   std::vector<std::string>::iterator m_current;    ///The questions   std::vector<std::string> m_questions; };  } //~namespace ribi  #endif // EXERCISE_H`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppExercise/exercise.cpp
--------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* Exercise, a collection of Questions Copyright (C) 2011-2015 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program.If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppExercise.htm //--------------------------------------------------------------------------- #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include "exercise.h"  #include <fstream> #include <stdexcept>   #include <boost/numeric/conversion/cast.hpp>  #include "fileio.h" #include "multiplechoicequestion.h" #include "multiplechoicequestiondialog.h" #include "openquestion.h" #include "openquestiondialog.h" #include "openquestiondialogfactory.h" //#include "trace.h"  #include <QFile>  #pragma GCC diagnostic pop  ribi::Exercise::Exercise(const std::string& filename)   : m_current{},     m_questions{} {   assert(QFile::exists(filename.c_str()));   if (!QFile::exists(filename.c_str()))   {     throw std::logic_error("File does not exist");   }   const std::vector<std::string> v {     ribi::fileio::FileIo().FileToVector(filename)   };   m_questions.reserve(v.size());   for(const std::string& s: v)   {     try     {       boost::shared_ptr<QuestionDialog> tmp         = OpenQuestionDialogFactory().Create(s);       m_questions.push_back(s);       continue;     }     catch (std::exception&)     {       //No problem     }     try     {       boost::shared_ptr<QuestionDialog> tmp(new MultipleChoiceQuestionDialog(s));       m_questions.push_back(s);       continue;     }     catch (std::exception&)     {       //No problem     }   }    if (m_questions.empty())   {     throw std::runtime_error("No questions found in loading the Exercise");   }   assert(!m_questions.empty());    //Shuffle the questions at start   std::random_shuffle(m_questions.begin(),m_questions.end());   m_current = m_questions.begin();   assert(m_current != m_questions.end()); }  std::string ribi::Exercise::GetCurrentQuestion() const noexcept {   assert(m_current != m_questions.end());   return *m_current; }  int ribi::Exercise::GetNumberOfQuestions() const noexcept {   assert(!m_questions.empty());   return boost::numeric_cast<int>(m_questions.size()); }  std::string ribi::Exercise::GetVersion() noexcept {   return "1.1"; }  std::vector<std::string> ribi::Exercise::GetVersionHistory() noexcept {   return {     "2011-09-26: Version 1.0: initial version",     "2011-10-30: Version 1.1: shuffle questions at start"   }; }  void ribi::Exercise::Next() noexcept {   ++m_current;   if (m_current == m_questions.end())   {     std::random_shuffle(m_questions.begin(),m_questions.end());     m_current = m_questions.begin();   } }`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)