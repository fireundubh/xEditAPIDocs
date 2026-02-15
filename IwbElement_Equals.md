# Equals

## Syntax

```pascal
function Equals(ASource: IwbElement; ATarget: IwbElement): boolean;
```

## Description

Compares two element references to determine if they point to the same element instance.

This function calls the first element's Equals method with the second element as the argument. Returns true if both references point to the exact same element object in memory. This is necessary because interface comparison with = can fail when different interface types wrap the same object. Use this for reliable element identity checking. Returns false for invalid elements or mismatched elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ASource | IwbElement | The first element to compare |
| ATarget | IwbElement | The second element to compare |

## Returns

Returns true if both elements have the same ElementID, false otherwise.

## Example

```pascal
// Example 1: Verify element identity
var
  element1, element2: IwbElement;
begin
  if Assigned(e) then begin
    element1 := ElementByPath(e, 'EDID');
    element2 := ElementByName(e, 'EDID');
    if Assigned(element1) and Assigned(element2) then begin
      if Equals(element1, element2) then
        AddMessage('Elements are the same instance')
      else
        AddMessage('Elements are different instances');
    end;
  end;
end;

// Example 2: Track unique elements during iteration
var
  container: IwbContainer;
  i, j: integer;
  element1, element2: IwbElement;
  duplicateFound: boolean;
begin
  if Assigned(e) then begin
    container := e;
    for i := 0 to ElementCount(container) - 1 do begin
      element1 := ElementByIndex(container, i);
      if Assigned(element1) then begin
        duplicateFound := False;
        for j := i + 1 to ElementCount(container) - 1 do begin
          element2 := ElementByIndex(container, j);
          if Assigned(element2) and Equals(element1, element2) then begin
            duplicateFound := True;
            Break;
          end;
        end;
        if not duplicateFound then
          AddMessage(Format('Element %d is unique', [i]));
      end;
    end;
  end;
end;

// Example 3: Compare references from different lookups
var
  byPath, byIndex, byName: IwbElement;
  container: IwbContainer;
begin
  if Assigned(e) then begin
    container := e;
    byPath := ElementByPath(e, 'EDID');
    byIndex := ElementByIndex(container, 0);
    byName := ElementByName(e, 'EDID');

    if Assigned(byPath) and Assigned(byIndex) and Assigned(byName) then begin
      if Equals(byPath, byIndex) and Equals(byIndex, byName) then
        AddMessage('All three lookups returned the same element')
      else begin
        AddMessage('Different lookups:');
        AddMessage(Format('  Path=Index: %s', [BoolToStr(Equals(byPath, byIndex), True)]));
        AddMessage(Format('  Index=Name: %s', [BoolToStr(Equals(byIndex, byName), True)]));
        AddMessage(Format('  Path=Name: %s', [BoolToStr(Equals(byPath, byName), True)]));
      end;
    end;
  end;
end;
```

## See Also

- [SortKey](IwbElement_SortKey.md)


