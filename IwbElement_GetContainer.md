# GetContainer

## Syntax

```pascal
function GetContainer(AElement: IwbElement): IwbContainer;
```

## Description

Returns the immediate parent container that holds this element.

This function retrieves the Container property, which provides access to the element's direct parent in the record hierarchy. For a field in a struct, this returns the struct. For a record, this returns the group. Returns nil if the element is at the top level or is invalid. Useful for navigating upward through the element tree.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the container for |

## Returns

Returns the immediate container as an IwbContainer interface.

## Example

```pascal
// Example 1: Navigate from child element to parent
var
  valueElement: IwbElement;
  dataContainer: IwbContainer;
  containerName: string;
begin
  if Assigned(e) then begin
    valueElement := ElementByPath(e, 'DATA\Value');
    if Assigned(valueElement) then begin
      dataContainer := GetContainer(valueElement);
      if Assigned(dataContainer) then begin
        containerName := Name(dataContainer);
        AddMessage(Format('Value element is in container: %s', [containerName]));
      end;
    end;
  end;
end;

// Example 2: Remove element from its parent
var
  unusedElement: IwbElement;
  parentContainer: IwbContainer;
begin
  if Assigned(e) then begin
    unusedElement := ElementByPath(e, 'MODL');
    if Assigned(unusedElement) then begin
      parentContainer := GetContainer(unusedElement);
      if Assigned(parentContainer) then begin
        AddMessage('Removing MODL from ' + Name(parentContainer));
        RemoveElement(parentContainer, unusedElement);
      end;
    end;
  end;
end;

// Example 3: Traverse hierarchy upward
var
  deepElement: IwbElement;
  container: IwbContainer;
  depth: integer;
begin
  if Assigned(e) then begin
    deepElement := ElementByPath(e, 'Conditions\[0]\CTDA\Function');
    if Assigned(deepElement) then begin
      depth := 0;
      container := GetContainer(deepElement);
      while Assigned(container) do begin
        Inc(depth);
        AddMessage(Format('Level %d: %s', [depth, Name(container)]));
        container := GetContainer(container);
      end;
      AddMessage(Format('Total depth: %d levels', [depth]));
    end;
  end;
end;
```

## See Also

- [ContainingMainRecord](IwbElement_ContainingMainRecord.md)
- [GetFile](IwbElement_GetFile.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementByName](IwbContainer_ElementByName.md)


