# frmMain

## Syntax

```pascal
function frmMain: TfrmMain;
```

## Description

Returns a reference to the main xEdit application window. This provides access to the primary user interface form and its properties and methods.

## Parameters

This function takes no parameters.

## Returns

Returns a TfrmMain object representing the main application window.

## Example

```pascal
var
  mainForm: TfrmMain;
begin
  mainForm := frmMain;
  AddMessage('Main form caption: ' + mainForm.Caption);
end;
```

## See Also

- [frmFileSelect](Global_frmFileSelect.md)
- [wbSettings](Global_wbSettings.md)
