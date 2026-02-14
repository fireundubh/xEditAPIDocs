# wbVersionNumber

## Syntax

```pascal
function wbVersionNumber: Cardinal;
```

## Description

Returns the version number of xEdit as a cardinal value. The version string is converted to a numerical representation for programmatic version checking.

## Parameters

This function takes no parameters.

## Returns

Returns a Cardinal representing the xEdit version number.

## Example

```pascal
var
  version: Cardinal;
begin
  version := wbVersionNumber;
  AddMessage('xEdit version number: ' + IntToStr(version));

  if version >= 4010000 then
    AddMessage('Running version 4.1.0 or higher');
end;
```

## See Also

- [wbAppName](Global_wbAppName.md)
