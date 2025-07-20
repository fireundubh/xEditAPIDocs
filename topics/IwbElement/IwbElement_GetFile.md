# GetFile

## Syntax

```pascal
function GetFile(AElement: IwbElement): IwbFile;
```

## Description

Returns the file that contains the element.

This function retrieves the plugin file (esp/esm/esl) that contains the specified element.

## Example

```pascal
var
  element: IwbElement;
  file: IwbFile;
begin
  file := GetFile(element);
  if Assigned(file) then
    // Work with the containing file
end;
```

## See Also

- [ContainingMainRecord](IwbElement_ContainingMainRecord.md)
