# MarkModifiedRecursive

## Syntax

```pascal
procedure MarkModifiedRecursive(AElement: IwbElement);
```

## Description

Marks the element and all of its descendants as modified.

This forces xEdit to serialize the marked elements. Useful when you've made changes to an element's hierarchy and need to ensure all changes are saved.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to mark as modified recursively |

## Example

```pascal
// Example 1: Force entire record to save
begin
  if Assigned(e) then begin
    MarkModifiedRecursive(e);
    AddMessage(Format('Marked %s and all children as modified', [EditorID(e)]));
  end;
end;

// Example 2: Ensure complex structure is saved after edits
var
  conditions: IwbContainer;
  i: integer;
  condition: IwbElement;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      BeginUpdate(conditions);
      try
        // Make multiple changes
        for i := 0 to ElementCount(conditions) - 1 do begin
          condition := ElementByIndex(conditions, i);
          if Assigned(condition) then
            SetElementEditValue(condition, 'CTDA\Comparison Value', '1.0');
        end;
        // Ensure all changes are saved
        MarkModifiedRecursive(conditions);
      finally
        EndUpdate(conditions);
      end;
      AddMessage(Format('Modified and marked %d conditions', [ElementCount(conditions)]));
    end;
  end;
end;

// Example 3: Mark after programmatic element creation
var
  newElement: IwbElement;
begin
  if Assigned(e) then begin
    newElement := Add(e, 'KWDA', True);
    if Assigned(newElement) then begin
      SetToDefault(newElement);
      SetElementEditValue(newElement, '[0]', '00012345');
      // Mark to ensure new structure is saved
      MarkModifiedRecursive(newElement);
      AddMessage(Format('Created and marked KWDA in %s', [EditorID(e)]));
    end;
  end;
end;
```

## See Also

- [Check](IwbElement_Check.md)


