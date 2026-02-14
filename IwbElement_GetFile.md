# GetFile

## Syntax

```pascal
function GetFile(AElement: IwbElement): IwbFile;
```

## Description

Returns the plugin file that contains this element.

This function retrieves the _File property, which provides access to the IwbFile interface representing the plugin (esp/esm/esl) that owns this element. All elements within a file hierarchy return the same file reference. Returns nil if the element is invalid or detached from a file.

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
- [GetContainer](IwbElement_GetContainer.md)
- [GetFileName](IwbFile_GetFileName.md)


