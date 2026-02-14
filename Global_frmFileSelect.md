# frmFileSelect

## Syntax

```pascal
function frmFileSelect: TfrmFileSelect;
```

## Description

Creates and returns a new instance of the file selection dialog form. This form allows users to select which plugin files to work with. The caller is responsible for managing the form's lifetime and disposal.

## Parameters

This function takes no parameters.

## Returns

Returns a TfrmFileSelect object representing a new file selection dialog instance.

## Example

```pascal
var
  fileSelectForm: TfrmFileSelect;
begin
  fileSelectForm := frmFileSelect;
  try
    if fileSelectForm.ShowModal = mrOk then
      AddMessage('User selected files from the dialog');
  finally
    fileSelectForm.Free;
  end;
end;
```

## See Also

- [frmMain](Global_frmMain.md)
