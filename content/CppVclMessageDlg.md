
 

 

 

 

 

([C++](Cpp.md)) [VCL MessageDlg](CppVclMessageDlg.md)
=======================================================

A [VCL dialog](CppVclDialog.md) posing a question that can be answered
by yes/no/cancel/etc.

 

To use [MessageDlg](CppVclMessageDlg.md), [\#include](CppInclude.md)
the [header file](CppHeaderFile.md) dialogs.hpp.

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` MessageDlg("You want me to give you this message?", //Message   mtConfirmation, //Message type   TMsgDlgButtons() << mbYes << mbNo, //Buttons   0); //Help Context`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Use of MessageDlg
-----------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` const int returnValue = MessageDlg(AnsiString Msg, //Message   TMsgDlgType DlgType, //Message type   TMsgDlgButtons Buttons, //Buttons   int HelpCtx); //Help context`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Possible return values are: mrOK, mrCancel, mrYes, mrNo, mrAbort,
mrRetry, mrIgnore

Possible message dialog types are:

 

  --------------------------------------------------------------------------------------
  ` enum TMsgDlgType { mtWarning, mtError, mtInformation, mtConfirmation, myCustom };`
  --------------------------------------------------------------------------------------

 

Possible buttons are:

 

  -----------------------------------------------------------------------------------------------------------------------
  ` enum TMsgDlgBtn { mbYes, mbNo, mbOK, mbCancel, mbAbort, mbRetry, mbIgnore, mbAll, mbNoToAll, mbYesToAll, mbHelp };`
  -----------------------------------------------------------------------------------------------------------------------

 

Because TMsgDlgButtons is a set, you use it e.g. by:

 

  --------------------------------------------------
  ` TMsgDlgButtons() << mbYes << mbNo; //Etcetera`
  --------------------------------------------------

 

 

 

 

 

 

