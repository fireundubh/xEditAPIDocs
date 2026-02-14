# ElementByPath

## Syntax

```pascal
function ElementByPath(AContainer: IwbContainer; APath: string): IwbElement;
```

## Description

Navigates through nested containers to find an element at the specified path.

This function accesses the ElementByPath property, which parses the path string and traverses the element hierarchy. Use backslash (\) as the separator for nested elements (e.g., "Model\MODL" finds the MODL element inside the Model struct). The path is resolved relative to the container. Returns nil if any part of the path doesn't exist. More flexible than ElementByName for accessing deeply nested elements.

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


