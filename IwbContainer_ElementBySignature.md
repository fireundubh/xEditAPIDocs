# ElementBySignature

## Syntax

```pascal
function ElementBySignature(AContainer: IwbContainer; ASignature: string): IwbElement;
```

## Description

Returns an element by its signature (record type) from the container. The signature is typically a 4-character identifier.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search for the element |
| ASignature | string | The 4-character signature of the element to retrieve |

## Returns

Returns the element with the specified signature as an IwbElement interface.

## Example

```pascal
// Example 1: Access subrecord by signature
var
  fullElement: IwbElement;
  displayName: string;
begin
  if Assigned(e) then begin
    fullElement := ElementBySignature(e, 'FULL');
    if Assigned(fullElement) then begin
      displayName := GetEditValue(fullElement);
      AddMessage('Display name: ' + displayName);
    end else
      AddMessage('No FULL subrecord found');
  end;
end;

// Example 2: Check multiple signature variants
var
  nameElement: IwbElement;
  name: string;
begin
  if Assigned(e) then begin
    // Try FULL first, fall back to EDID
    nameElement := ElementBySignature(e, 'FULL');
    if not Assigned(nameElement) then
      nameElement := ElementBySignature(e, 'EDID');

    if Assigned(nameElement) then begin
      name := GetEditValue(nameElement);
      AddMessage('Name: ' + name);
    end else
      AddMessage('No name found');
  end;
end;

// Example 3: Access model data by signature
var
  modelContainer: IwbContainer;
  modlElement, modb Element, modtElement: IwbElement;
  modelPath, bounds, textureHash: string;
begin
  if Assigned(e) then begin
    modelContainer := ElementByPath(e, 'Model');
    if Assigned(modelContainer) then begin
      modlElement := ElementBySignature(modelContainer, 'MODL');
      if Assigned(modlElement) then begin
        modelPath := GetEditValue(modlElement);
        AddMessage('Model: ' + modelPath);
      end;

      modbElement := ElementBySignature(modelContainer, 'MODB');
      if Assigned(modbElement) then begin
        bounds := GetEditValue(modbElement);
        AddMessage('Bounds: ' + bounds);
      end;

      modtElement := ElementBySignature(modelContainer, 'MODT');
      if Assigned(modtElement) then begin
        textureHash := GetEditValue(modtElement);
        AddMessage('Texture data hash: ' + textureHash);
      end;
    end;
  end;
end;
```

## See Also

- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementByName](IwbContainer_ElementByName.md)
- [ElementByPath](IwbContainer_ElementByPath.md)
- [GroupBySignature](IwbFile_GroupBySignature.md)


