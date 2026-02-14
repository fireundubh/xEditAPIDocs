# GetFile

## Syntax

```pascal
function GetFile(AElement: IwbElement): IwbFile;
```

## Description

Returns the file that contains the element.

This function retrieves the plugin file (esp/esm/esl) that contains the specified element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the containing file for |

## Returns

Returns the containing file as an IwbFile interface.

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


