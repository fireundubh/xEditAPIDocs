# ContainingMainRecord

## Syntax

```pascal
function ContainingMainRecord(AElement: IwbElement): IwbMainRecord;
```

## Description

Returns the IwbMainRecord that owns this element in the record hierarchy.

This function retrieves the ContainingMainRecord property, which traverses up the element tree to find the nearest IwbMainRecord ancestor. For subrecords and nested elements, this returns the record they belong to. For main records, this returns the record itself. Returns nil for elements not part of a main record (like file headers or groups). Useful for navigating from field-level elements to their owning record.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the containing main record for |

## Returns

Returns the containing main record as an IwbMainRecord interface.

## Example

```pascal
// Example 1: Navigate from deep element to owning record
var
  conditionFunc: IwbElement;
  owningRecord: IwbMainRecord;
  ownerEdid: string;
begin
  if Assigned(e) then begin
    conditionFunc := ElementByPath(e, 'Conditions\[0]\CTDA\Function');
    if Assigned(conditionFunc) then begin
      owningRecord := ContainingMainRecord(conditionFunc);
      if Assigned(owningRecord) then begin
        ownerEdid := EditorID(owningRecord);
        AddMessage(Format('Condition function belongs to record: %s', [ownerEdid]));
      end;
    end;
  end;
end;

// Example 2: Check element ownership when processing containers
var
  effects: IwbContainer;
  i: integer;
  effectElement: IwbElement;
  parentRecord: IwbMainRecord;
begin
  if Assigned(e) then begin
    effects := ElementByPath(rec, 'Effects');
    if Assigned(effects) then begin
      for i := 0 to ElementCount(effects) - 1 do begin
        effectElement := ElementByIndex(effects, i);
        if Assigned(effectElement) then begin
          parentRecord := ContainingMainRecord(effectElement);
          if Assigned(parentRecord) then
            AddMessage(Format('Effect %d parent: %s', [i, EditorID(parentRecord)]));
        end;
      end;
    end;
  end;
end;

// Example 3: Get record context for error reporting
var
  dataValue: IwbElement;
  owningRec: IwbMainRecord;
  recFile: IwbFile;
  fileName, edid: string;
  value: integer;
begin
  if Assigned(e) then begin
    dataValue := ElementByPath(rec, 'DATA\Value');
    if Assigned(dataValue) then begin
      value := GetNativeValue(dataValue);
      if value < 0 then begin
        owningRec := ContainingMainRecord(dataValue);
        if Assigned(owningRec) then begin
          edid := EditorID(owningRec);
          recFile := GetFile(owningRec);
          if Assigned(recFile) then
            fileName := GetFileName(recFile);
          AddMessage(Format('ERROR: Negative value %d in %s [%s]',
            [value, edid, fileName]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [GetContainer](IwbElement_GetContainer.md)
- [GetFile](IwbElement_GetFile.md)
- [EditorID](IwbMainRecord_EditorID.md)
- [FormID](IwbMainRecord_FormID.md)


