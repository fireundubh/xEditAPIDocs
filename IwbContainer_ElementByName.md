# ElementByName

## Syntax

```pascal
function ElementByName(AContainer: IwbContainer; AName: string): IwbElement;
```

## Description

Searches the container for a child element with the specified name.

This function accesses the ElementByName property, which searches for an element whose Name property matches the provided string. The search is typically case-sensitive and looks at the element's definition name (e.g., "EDID", "DATA"). Returns nil if no element with that name exists in the container. For nested paths, use ElementByPath instead.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search for the element |
| AName | string | The name of the element to retrieve |

## Returns

Returns the element with the specified name as an IwbElement interface.

## Example

```pascal
// Example 1: Access struct field by name
var
  dataElement: IwbElement;
  value, weight: string;
begin
  if Assigned(e) then begin
    dataElement := ElementByName(e, 'DATA');
    if Assigned(dataElement) then begin
      // DATA is a container, access its fields by name
      value := GetEditValue(ElementByName(dataElement, 'Value'));
      weight := GetEditValue(ElementByName(dataElement, 'Weight'));
      AddMessage(Format('Value: %s, Weight: %s', [value, weight]));
    end;
  end;
end;

// Example 2: Get common record fields by name
var
  edidElement, fullElement: IwbElement;
  editorID, displayName: string;
begin
  if Assigned(e) then begin
    edidElement := ElementByName(e, 'EDID');
    if Assigned(edidElement) then
      editorID := GetEditValue(edidElement)
    else
      editorID := '(no editor ID)';

    fullElement := ElementByName(e, 'FULL');
    if Assigned(fullElement) then
      displayName := GetEditValue(fullElement)
    else
      displayName := '(no display name)';

    AddMessage(Format('EDID: %s, FULL: %s', [editorID, displayName]));
  end;
end;

// Example 3: Iterate struct fields by name
var
  modelContainer: IwbContainer;
  modlElement, modtElement: IwbElement;
  modelPath, textureHash: string;
begin
  if Assigned(e) then begin
    modelContainer := ElementByPath(e, 'Model');
    if Assigned(modelContainer) then begin
      // Access nested fields by name
      modlElement := ElementByName(modelContainer, 'MODL');
      if Assigned(modlElement) then begin
        modelPath := GetEditValue(modlElement);
        AddMessage('Model path: ' + modelPath);
      end;

      modtElement := ElementByName(modelContainer, 'MODT');
      if Assigned(modtElement) then begin
        textureHash := GetEditValue(modtElement);
        AddMessage('Texture hash: ' + textureHash);
      end;
    end;
  end;
end;
```

## See Also

- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementByPath](IwbContainer_ElementByPath.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)
- [ElementExists](IwbContainer_ElementExists.md)
- [IndexOf](IwbContainer_IndexOf.md)


