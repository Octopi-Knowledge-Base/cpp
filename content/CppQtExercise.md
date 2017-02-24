

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [QtExercise](CppQtExercise.htm)
================================================

 

![Qt](PicQt.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)

 

[QtExercise](CppQtExercise.htm) is a [Qt](CppQt.htm)
[class](CppClass.htm) to display an [Exercise](CppExercise.htm).

Technical facts
---------------

 

 

 

 

 

 

./CppQtExercise/CppQtExercise.pri
---------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppQtExercise  SOURCES += \     ../../Classes/CppQtExercise/qtexercise.cpp  HEADERS  += \     ../../Classes/CppQtExercise/qtexercise.h  OTHER_FILES += \     ../../Classes/CppQtExercise/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExercise/qtexercise.h
----------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* QtExercise, Qt GUI of Exercise Copyright (C) 2012-2014 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program.If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppQtExercise.htm //--------------------------------------------------------------------------- #ifndef QTEXERCISE_H #define QTEXERCISE_H  #include <string> #include <vector>  #include <boost/shared_ptr.hpp>  #include "qthideandshowdialog.h"  struct QGroupBox; struct QLabel;  namespace ribi {  struct Exercise;  ///A QtExercise is the Qt dialog of Exercise struct QtExercise : public QtHideAndShowDialog {   ///Construct a QtExercise without questions   QtExercise();   ~QtExercise() noexcept {}    ///Obtain the user its score: its number of correctly answered   ///questions and the total number of questions answered   const std::pair<int,int> GetCurrentScore() const;    ///Get the Exercise   const Exercise * GetExercise() const;    ///Obtain this class its version   static std::string GetVersion() noexcept;    ///Obtain this class its version history   static std::vector<std::string> GetVersionHistory() noexcept;    ///Set the questions, read from a file   ///Throws std::logic_error if file does not exist   ///Throws std::runtime_error if file does not contain a single question   void SetQuestions(const std::string& filename);    ///Set the time the user has to wait when he/she answered correctly, in milliseconds   void SetWaitingTimeCorrect(const int msecs);    ///Set the time the user has to wait when he/she answered incorrectly, in milliseconds   void SetWaitingTimeIncorrect(const int msecs);    private:   ///The Exercise   boost::shared_ptr<Exercise> m_exercise;    ///The number of answered questions   int m_n_answered;    ///The number of correctly answered questions   int m_n_correct;    struct MyUi   {     MyUi();     QGroupBox * const m_box;     QLabel * const m_label_score;   } m_ui;    ///The time the user has to wait when he/she answered correctly, in milliseconds   int m_waiting_time_correct;    ///The time the user has to wait when he/she answered incorrectly, in milliseconds   int m_waiting_time_incorrect;    ///Displays m_dialog its current question   void DisplayCurrentQuestion();    ///Respond to the client having answered a question   void OnSubmittedAnswer(const bool answered_correct);    ///Respond to the client having viewed the answer of a question   void OnViewedAnswer(); };  } //~namespace ribi  #endif // QTEXERCISE_H`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtExercise/qtexercise.cpp
------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` //--------------------------------------------------------------------------- /* QtExercise, Qt GUI of Exercise Copyright (C) 2011-2014 Richel Bilderbeek  This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.  This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.See the GNU General Public License for more details. You should have received a copy of the GNU General Public License along with this program.If not, see <http://www.gnu.org/licenses/>. */ //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppQtExercise.htm //--------------------------------------------------------------------------- #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #pragma GCC diagnostic ignored "-Wunused-but-set-parameter" #include "qtexercise.h"  #include <fstream>  #include <boost/bind.hpp> #include <boost/lambda/lambda.hpp> #include <boost/signals2.hpp>  #include <QGroupBox> #include <QLabel> #include <QTimer> #include <QVBoxLayout>  #include "exercise.h" #include "multiplechoicequestiondialog.h" #include "openquestiondialog.h" #include "openquestiondialogfactory.h" #include "qtmultiplechoicequestiondialog.h" #include "qtopenquestiondialog.h" #include "qtquestiondialog.h" #include "trace.h" #pragma GCC diagnostic pop  ribi::QtExercise::MyUi::MyUi()   : m_box(new QGroupBox),     m_label_score(new QLabel) {  }  ribi::QtExercise::QtExercise()   : m_exercise{},     m_n_answered(0),     m_n_correct(0),     m_ui{},     m_waiting_time_correct(1000),     m_waiting_time_incorrect(5000) {   assert(m_ui.m_box);   assert(m_ui.m_label_score);    QVBoxLayout * const layout = new QVBoxLayout;   this->setLayout(layout);   layout->addWidget(m_ui.m_box);   layout->addWidget(m_ui.m_label_score);    m_ui.m_label_score->setText("Score: 0/0"); }  void ribi::QtExercise::DisplayCurrentQuestion() {   const std::string s = m_exercise->GetCurrentQuestion();    boost::shared_ptr<QtQuestionDialog> question;   try   {     const boost::shared_ptr<OpenQuestionDialog> d = OpenQuestionDialogFactory().Create(s);     //const boost::shared_ptr<OpenQuestionDialog> d(new OpenQuestionDialog(s));     //question = new QtOpenQuestionDialog(d);     const auto p = boost::make_shared<QtOpenQuestionDialog>();     p->SetDialog(d);     question = p;    }   catch(std::exception&) {}   if (!question)   {     try     {       const boost::shared_ptr<MultipleChoiceQuestionDialog> d(new MultipleChoiceQuestionDialog(s));       //question = new QtMultipleChoiceQuestionDialog(d);       question = boost::make_shared<QtMultipleChoiceQuestionDialog>(d);     }     catch(std::exception&) {}   }   assert(question && "Exercise only contains valid question");    //Add QtQuestionDialog   assert(m_ui.m_box);   if (m_ui.m_box->layout()) delete m_ui.m_box->layout();   QVBoxLayout * const layout = new QVBoxLayout;   m_ui.m_box->setLayout(layout);   layout->addWidget(question.get());    question->GetDialog()->m_signal_submitted.connect(     boost::bind(&ribi::QtExercise::OnSubmittedAnswer,this,boost::lambda::_1)   );  }  const ribi::Exercise * ribi::QtExercise::GetExercise() const {   assert(m_exercise);   return m_exercise.get(); }  std::string ribi::QtExercise::GetVersion() noexcept {   return "1.0"; }  std::vector<std::string> ribi::QtExercise::GetVersionHistory() noexcept {   return {     "2012-12-23: Version 1.0: initial version"   }; }  void ribi::QtExercise::OnSubmittedAnswer(const bool answered_correct) {   if (answered_correct) ++m_n_correct;   ++m_n_answered;   m_ui.m_label_score->setText(     QString("Score: {1}/{2}").arg(m_n_correct).arg(m_n_answered));   QTimer::singleShot(     answered_correct ? m_waiting_time_correct : m_waiting_time_incorrect,     this,     SLOT(&ribi::QtExercise::OnViewedAnswer)); }  void ribi::QtExercise::OnViewedAnswer() {   this->m_exercise->Next();   this->DisplayCurrentQuestion(); }  void ribi::QtExercise::SetQuestions(const std::string& filename) {   m_exercise.reset(new Exercise(filename));   DisplayCurrentQuestion(); }  void ribi::QtExercise::SetWaitingTimeCorrect(const int msecs) {   assert(msecs >= 0);   m_waiting_time_correct = msecs; }  void ribi::QtExercise::SetWaitingTimeIncorrect(const int msecs) {   assert(msecs >= 0);   m_waiting_time_incorrect = msecs; }`
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)