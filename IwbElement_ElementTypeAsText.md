# ElementTypeAsText

## Syntax

```pascal
function ElementTypeAsText(AElement: IwbElement): String;
```

## Description

Returns the element type of `AElement` as a string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the element type from |

## Returns

Returns the element type as a string.

## Example

```pascal
// Example 1: Log element types during iteration
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  typeName: string;
begin
  if Assigned(e) then begin
    container := e;
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        typeName := ElementTypeAsText(element);
        AddMessage(Format('[%d] %s - Type: %s',
          [i, Name(element), typeName]));
      end;
    end;
  end;
end;

// Example 2: Filter elements by type string
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  typeText: string;
  arrayCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    arrayCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        typeText := ElementTypeAsText(element);
        if typeText = 'etArray' then begin
          Inc(arrayCount);
          AddMessage(Format('Array: %s', [Name(element)]));
        end;
      end;
    end;

    AddMessage(Format('Found %d array elements', [arrayCount]));
  end;
end;

// Example 3: Build type distribution report
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  typeText: string;
  typeList: TStringList;
begin
  if Assigned(e) then begin
    container := e;
    typeList := TStringList.Create;
    try
      typeList.Sorted := True;
      typeList.Duplicates := dupIgnore;

      for i := 0 to ElementCount(container) - 1 do begin
        element := ElementByIndex(container, i);
        if Assigned(element) then begin
          typeText := ElementTypeAsText(element);
          typeList.Add(typeText);
        end;
      end;

      AddMessage(Format('Element types in %s:', [EditorID(e)]));
      for i := 0 to typeList.Count - 1 do
        AddMessage('  ' + typeList[i]);
    finally
      typeList.Free;
    end;
  end;
end;
```

## See Also

- [ElementType](IwbElement_ElementType.md)
- [DefTypeAsText](IwbElement_DefTypeAsText.md)
