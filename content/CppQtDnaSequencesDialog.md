

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [QtDnaSequencesDialog](CppQtDnaSequencesDialog.htm)
====================================================================

 

Technical facts
---------------

 

 

 

 

 

 

./CppQtDnaSequencesDialog/CppQtDnaSequencesDialog.pri
-----------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppQtDnaSequencesDialog  SOURCES += \     ../../Classes/CppQtDnaSequencesDialog/qtdnasequencesdialog.cpp  HEADERS  += \     ../../Classes/CppQtDnaSequencesDialog/qtdnasequencesdialog.h  FORMS += \     ../../Classes/CppQtDnaSequencesDialog/qtdnasequencesdialog.ui  OTHER_FILES += \     ../../Classes/CppQtDnaSequencesDialog/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtDnaSequencesDialog/qtdnasequencesdialog.h
------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTDNASEQUENCESDIALOG_H #define QTDNASEQUENCESDIALOG_H  #include <QWidget>  namespace ribi { struct DnaSequence; } namespace Ui { class QtDnaSequencesDialog; }  class QtDnaSequencesDialog : public QWidget {   Q_OBJECT  public:   explicit QtDnaSequencesDialog(QWidget *parent = 0);   QtDnaSequencesDialog(const QtDnaSequencesDialog&) = delete;   QtDnaSequencesDialog& operator=(const QtDnaSequencesDialog&) = delete;   ~QtDnaSequencesDialog();    std::vector<ribi::DnaSequence> GetSequences() const noexcept;   //void SetDnaSequences(const std::vector<ribi::DnaSequence>& sequences) noexcept;  private:   Ui::QtDnaSequencesDialog *ui;    static const std::string sm_fail; };  #endif // QTDNASEQUENCESDIALOG_H`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtDnaSequencesDialog/qtdnasequencesdialog.cpp
--------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "qtdnasequencesdialog.h"  #include <cassert> #include <functional> #include <QLabel>  #include "dnasequence.h" #include "fileio.h" #include "ui_qtdnasequencesdialog.h" #include "dna_r.h"  const std::string QtDnaSequencesDialog::sm_fail{":-("};  QtDnaSequencesDialog::QtDnaSequencesDialog(QWidget *parent) :   QWidget(parent),   ui(new Ui::QtDnaSequencesDialog) {   ui->setupUi(this); }  QtDnaSequencesDialog::~QtDnaSequencesDialog() {   delete ui; }  std::vector<ribi::DnaSequence> QtDnaSequencesDialog::GetSequences() const noexcept {   using ribi::DnaSequence;   std::vector<DnaSequence> sequences;   sequences.push_back(DnaSequence(ui->edit_name_1->text().toStdString(),ui->edit_sequence_1->text().toStdString()));   sequences.push_back(DnaSequence(ui->edit_name_2->text().toStdString(),ui->edit_sequence_2->text().toStdString()));   sequences.push_back(DnaSequence(ui->edit_name_3->text().toStdString(),ui->edit_sequence_3->text().toStdString()));   sequences.push_back(DnaSequence(ui->edit_name_4->text().toStdString(),ui->edit_sequence_4->text().toStdString()));   return sequences; }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)

This page has been created by the [tool](Tools.htm)
[CodeToHtml](ToolCodeToHtml.htm)