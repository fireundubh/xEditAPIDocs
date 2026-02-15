# IsEditable

## Syntax

```pascal
function IsEditable(AElement: IwbElement): boolean;
```

## Description

Checks if an element can be edited.

Returns true if the element can be modified. Some elements, particularly those in base game master files like Skyrim.esm, may be locked from editing.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check if it's editable |

## Returns

Returns true if the element can be edited, false otherwise.

## Example

```pascal
// Example 1: Safe element modification
var
  edidElement: IwbElement;
begin
  if Assigned(e) then begin
    edidElement := ElementByPath(e, 'EDID');
    if Assigned(edidElement) then begin
      if IsEditable(edidElement) then begin
        SetEditValue(edidElement, 'NewEditorID');
        AddMessage('Successfully changed EDID');
      end else
        AddMessage('EDID is not editable (master file)');
    end;
  end;
end;

// Example 2: Filter editable records for batch processing
var
  pluginFile: IwbFile;
  fileName: string;
begin
  if Assigned(e) then begin
    if IsEditable(e) then begin
      // Process editable record
      SetElementEditValue(e, 'DATA\Value', '100');
      AddMessage(Format('Modified %s', [EditorID(e)]));
    end else begin
      pluginFile := GetFile(e);
      if Assigned(pluginFile) then
        fileName := GetFileName(pluginFile);
      AddMessage(Format('Skipped %s (locked in %s)', [EditorID(e), fileName]));
    end;
  end;
end;

// Example 3: Create override if original is not editable
var
  override: IwbMainRecord;
  targetFile: IwbFile;
  valueElement: IwbElement;
begin
  if Assigned(e) then begin
    if not IsEditable(e) then begin
      targetFile := FileByIndex(FileCount - 1);
      if Assigned(targetFile) then begin
        override := wbCopyElementToFile(e, targetFile, False, True);
        if Assigned(override) then begin
          AddMessage(Format('Created override for %s', [EditorID(e)]));
          valueElement := ElementByPath(override, 'DATA\Value');
          if Assigned(valueElement) and IsEditable(valueElement) then begin
            SetEditValue(valueElement, '100');
            AddMessage('Modified override value');
          end;
        end;
      end;
    end else begin
      // Direct modification
      SetElementEditValue(e, 'DATA\Value', '100');
      AddMessage(Format('Modified original %s', [EditorID(e)]));
    end;
  end;
end;
```

## See Also

- [SetEditValue](IwbElement_SetEditValue.md)
- [SetElementState](IwbElement_SetElementState.md)


