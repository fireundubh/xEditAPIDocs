# Remove

## Syntax

```pascal
procedure Remove(AElement: IwbElement);
```

## Description

Removes the element from its parent container.

This function calls the element's Remove method, which detaches it from its parent container and marks it for deletion. The element is removed from memory immediately, but the change is not persisted to disk until the file is saved. This operation is irreversible once the file is saved.

Use with caution. Removing critical elements may corrupt the record structure or make the file invalid.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to remove from its file |

## Example

```pascal
// Example 1: Remove unwanted subrecord
var
  rec: IwbMainRecord;
  modelElement: IwbElement;
begin
  if Assigned(e) then begin
    modelElement := ElementByPath(rec, 'MODL');
    if Assigned(modelElement) then begin
      AddMessage(Format('Removing model from %s', [EditorID(e)]));
      Remove(modelElement);
    end;
  end;
end;

// Example 2: Clean up empty or invalid array elements
var
  rec: IwbMainRecord;
  keywords: IwbContainer;
  i: integer;
  kwdElement: IwbElement;
  kwdRecord: IwbMainRecord;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(rec, 'KWDA');
    if Assigned(keywords) then begin
      // Iterate backwards when removing to avoid index shifts
      for i := ElementCount(keywords) - 1 downto 0 do begin
        kwdElement := ElementByIndex(keywords, i);
        if Assigned(kwdElement) then begin
          kwdRecord := LinksTo(kwdElement);
          if not Assigned(kwdRecord) then begin
            AddMessage(Format('Removing invalid keyword at index %d', [i]));
            Remove(kwdElement);
          end;
        end;
      end;
    end;
  end;
end;

// Example 3: Remove specific conditions
var
  rec: IwbMainRecord;
  conditions: IwbContainer;
  i: integer;
  condition, funcElement: IwbElement;
  funcValue: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(rec, 'Conditions');
    if Assigned(conditions) then begin
      for i := ElementCount(conditions) - 1 downto 0 do begin
        condition := ElementByIndex(conditions, i);
        if Assigned(condition) then begin
          funcElement := ElementByPath(condition, 'CTDA\Function');
          if Assigned(funcElement) then begin
            funcValue := GetEditValue(funcElement);
            if funcValue = 'GetDead' then begin
              AddMessage(Format('Removing GetDead condition from %s', [EditorID(e)]));
              Remove(condition);
            end;
          end;
        end;
      end;
    end;
  end;
end;
```

## See Also

- [RemoveByIndex](IwbContainer_RemoveByIndex.md)
- [RemoveElement](IwbContainer_RemoveElement.md)


