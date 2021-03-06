
 

 

 

 

 

([C++](Cpp.md)) [Wt::WCssStyleSheet](CppWCssStyleSheet.md)
============================================================

 

[Wt::WCssStyleSheet](CppWCssStyleSheet.md) is a [Wt](CppWt.md)
[class](CppClass.md) to use a cascading style sheet.

 

The stylesheet of an application is set in
[Wt::WApplication](CppWApplication.md), in multiple ways:

-   By loading a css file
-   By adding all css rules in code

 

Both options are shown below.

 

 

 

 

 

Loading a css file
------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` Wt::WCssStyleSheet  struct MyApplication : public Wt::WApplication {   MyApplication(const Wt::WEnvironment& env)     : Wt::WApplication(env)   {     this->useStyleSheet("my_stylesheet.css");   } }; `
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

An example of 'my\_stylesheet.css' is:

 

  ------------------------------------------------------------------------------
  ` body { font-family:"Courier New"; } button { font-family:"Courier New"; }`
  ------------------------------------------------------------------------------

 

 

 

 

 

Adding css rules in code
------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` struct MyApplication : public Wt::WApplication {   MyApplication(const Wt::WEnvironment& env)     : Wt::WApplication(env)   {     this->styleSheet().addRule("body","font-family: \"Courier New\"");     this->styleSheet().addRule("button","font-family: \"Courier New\"");   } };`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

These css rules are identical to the loaded css rules shown above.

 

 

 

 

 

[Wt](CppWt.md) widget tags
---------------------------

 

From \[1\].

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` WAnchor - a; WBreak - br; WCheckBox - input; WComboBox - option and select; WContainerWidget - div; WFileUpload - form and input; WGroupBox - fieldset and legend; WImage - img; WLabel - label; WLineEdit - input; WPushButton - button; WRadioButton - input; WScrollArea - div (probably with "overflow: scroll" style); WTable - table, tbody, tr; WTableCell - td; WText - span, sometimes two nested spans; WTextArea - textarea; WTimerWidget - span.`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

[References](CppReferences.md)
-------------------------------

 

1.  ['Using CSS' tutorial on Wt
    wiki](http://redmine.webtoolkit.eu/projects/wt/wiki/Using_CSS)

 

 

 

 

 

 

