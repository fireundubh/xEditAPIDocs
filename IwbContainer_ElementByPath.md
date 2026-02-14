# ElementByPath

## Syntax

```pascal
function ElementByPath(AContainer: IwbContainer; APath: string): IwbElement;
```

## Description

Returns an element by its path from the container. The path is a string representing the hierarchical location of the element, using backslash (`\`) as the path separator for nested elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search within |
| APath | string | The hierarchical path to the desired element (e.g., `'Model\MODL'`) |

## Returns

Returns the IwbElement at the specified path, or `nil` if the path doesn't exist.

## Example

```pascal
var
  record: IwbMainRecord;
  modelElement: IwbElement;
  modelPath: string;
begin
  record := RecordByFormID(FileByIndex(0), $00012345, True);
  modelElement := ElementByPath(record, 'Model\MODL');
  if Assigned(modelElement) then begin
    modelPath := GetEditValue(modelElement);
    AddMessage('Model path: ' + modelPath);
  end;
end;
```

## See Also

- [ElementByName](IwbContainer_ElementByName.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementExists](IwbContainer_ElementExists.md)


