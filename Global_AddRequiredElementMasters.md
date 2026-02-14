# AddRequiredElementMasters

## Syntax

```pascal
function AddRequiredElementMasters(AElement: IwbElement; AFile: IwbFile; AAsNew: Boolean; ASilent: Boolean = False): Boolean;
```

## Description

Adds all master files required by an element to a target file. This function analyzes the element's dependencies and ensures the target file has all necessary master references before copying or working with the element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose required masters will be analyzed |
| AFile | IwbFile | The target file that will receive the master references |
| AAsNew | Boolean | Whether to add masters as new entries |
| ASilent | Boolean | Optional. If True, suppresses confirmation dialogs. Defaults to False |

## Returns

Returns True if the required masters were successfully added to the target file, False otherwise.

## Example

```pascal
var
  sourceElement: IwbElement;
  targetFile: IwbFile;
begin
  sourceElement := RecordByFormID(FileByIndex(0), $00012345);
  targetFile := FileByIndex(1);

  if AddRequiredElementMasters(sourceElement, targetFile, True, False) then
    AddMessage('Required masters added successfully');
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
