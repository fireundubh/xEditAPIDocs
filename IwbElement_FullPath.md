# FullPath

## Syntax

```pascal
function FullPath(AElement: IwbElement): string;
```

## Description

Returns the complete hierarchical path from the file root to this element.

This function retrieves the FullPath property, which builds the full path string by traversing from the element up through all parent containers to the file. The path uses backslash separators and includes the filename at the start (e.g., "Skyrim.esm\WEAP\[00012345]\EDID"). Useful for logging, debugging, and uniquely identifying elements. Returns an empty string for invalid elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the full path for |

## Returns

Returns the complete hierarchical path as a string.

## Example

```pascal
// Example 1: Log element location for debugging
var
  rec: IwbMainRecord;
  element: IwbElement;
  elementPath: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA\Value');
    if Assigned(element) then begin
      elementPath := FullPath(element);
      AddMessage(Format('Full path: %s', [elementPath]));
      // Output: "Skyrim.esm\WEAP\[00012EB7]\DATA - Data\Value"
    end;
  end;
end;

// Example 2: Track element changes with full context
var
  rec: IwbMainRecord;
  edidElement: IwbElement;
  oldPath, newPath: string;
  oldValue, newValue: string;
begin
  if Assigned(e) then begin
    edidElement := ElementByPath(e, 'EDID');
    if Assigned(edidElement) then begin
      oldPath := FullPath(edidElement);
      oldValue := GetEditValue(edidElement);
      SetEditValue(edidElement, 'NewEditorID');
      newValue := GetEditValue(edidElement);
      AddMessage(Format('Changed %s: "%s" -> "%s"',
        [oldPath, oldValue, newValue]));
    end;
  end;
end;

// Example 3: Build error report with precise locations
var
  rec: IwbMainRecord;
  conditions: IwbContainer;
  i: integer;
  condition, funcElement: IwbElement;
  funcPath: string;
  funcValue: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      for i := 0 to ElementCount(conditions) - 1 do begin
        condition := ElementByIndex(conditions, i);
        if Assigned(condition) then begin
          funcElement := ElementByPath(condition, 'CTDA\Function');
          if Assigned(funcElement) then begin
            funcValue := GetEditValue(funcElement);
            if funcValue = '' then begin
              funcPath := FullPath(funcElement);
              AddMessage(Format('ERROR: Empty function at %s', [funcPath]));
            end;
          end;
        end;
      end;
    end;
  end;
end;
```

## See Also

- [Path](IwbElement_Path.md)
- [IndexedPath](IwbElement_IndexedPath.md)
- [PathName](IwbElement_PathName.md)
- [Name](IwbElement_Name.md)


