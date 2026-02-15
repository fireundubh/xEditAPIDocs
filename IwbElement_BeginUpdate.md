# BeginUpdate

## Syntax

```pascal
procedure BeginUpdate(AElement: IwbElement);
```

## Description

Begins an update batch for the element to defer notifications and improve performance.

This function calls the element's BeginUpdate method, which increments an internal update counter. While in update mode, the element defers change notifications and UI updates. Multiple BeginUpdate calls can be nested, and each must be matched with a corresponding EndUpdate. Always use in a try-finally block to ensure EndUpdate is called. Returns the new update counter value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to begin bulk updates on |

## Example

```pascal
// Example 1: Batch update record properties
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      SetElementEditValue(e, 'EDID', 'NewEditorID');
      SetElementEditValue(e, 'FULL', 'New Display Name');
      SetElementEditValue(e, 'DATA\Value', '250');
      SetElementEditValue(e, 'DATA\Weight', '15.5');
      // All notifications deferred until EndUpdate
    finally
      EndUpdate(e);
    end;
  end;
end;

// Example 2: Batch add array elements
var
  keywords: IwbContainer;
  i: integer;
  keywordIDs: array of string;
begin
  if Assigned(e) then begin
    // Prepare keyword FormIDs
    SetLength(keywordIDs, 5);
    keywordIDs[0] := '000424A';
    keywordIDs[1] := '000424B';
    keywordIDs[2] := '000424C';
    keywordIDs[3] := '000424D';
    keywordIDs[4] := '000424E';

    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      BeginUpdate(keywords);
      try
        for i := 0 to High(keywordIDs) do begin
          SetElementEditValue(keywords, '[' + IntToStr(i) + ']', keywordIDs[i]);
        end;
      finally
        EndUpdate(keywords);
      end;
    end;
  end;
end;

// Example 3: Nested BeginUpdate (parent and child)
var
  conditions: IwbContainer;
  condition: IwbElement;
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      conditions := ElementByPath(e, 'Conditions');
      if Assigned(conditions) then begin
        BeginUpdate(conditions);
        try
          condition := Add(conditions, 'Condition', true);
          SetElementEditValue(condition, 'CTDA\Type', '10000000');
          SetElementEditValue(condition, 'CTDA\Comparison Value', '1');
        finally
          EndUpdate(conditions);
        end;
      end;
    finally
      EndUpdate(e);
    end;
  end;
end;
```

## See Also

- [EndUpdate](IwbElement_EndUpdate.md)
