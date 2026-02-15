# EndUpdate

## Syntax

```pascal
procedure EndUpdate(AElement: IwbElement);
```

## Description

Ends an update batch for the element and processes any deferred notifications.

This function calls the element's EndUpdate method, which decrements the internal update counter. When the counter reaches zero, all deferred change notifications are processed and the element is marked as modified. Must be called once for each BeginUpdate. Always use in a try-finally block to guarantee execution even if errors occur during updates.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to end bulk updates on |

## Example

```pascal
// Example 1: Basic update block
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      SetElementEditValue(e, 'EDID', 'NewEditorID');
      SetElementEditValue(e, 'FULL', 'New Display Name');
      SetElementEditValue(e, 'DATA\Value', '100');
    finally
      EndUpdate(e);
    end;
    AddMessage('Batch update completed');
  end;
end;

// Example 2: Nested updates with error handling
var
  conditions: IwbContainer;
  i: integer;
  condition: IwbElement;
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      conditions := ElementByPath(e, 'Conditions');
      if Assigned(conditions) then begin
        BeginUpdate(conditions);
        try
          for i := 0 to ElementCount(conditions) - 1 do begin
            condition := ElementByIndex(conditions, i);
            if Assigned(condition) then
              SetElementEditValue(condition, 'CTDA\Comparison Value', '1.0');
          end;
        finally
          EndUpdate(conditions);
        end;
      end;
    finally
      EndUpdate(e);
    end;
  end;
end;

// Example 3: Update with validation
var
  errorMsg: string;
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      SetElementEditValue(e, 'DATA\Value', '250');
      SetElementEditValue(e, 'DATA\Weight', '15.5');

      // Validate before committing
      errorMsg := Check(e);
      if errorMsg <> '' then
        AddMessage(Format('WARNING: %s', [errorMsg]));
    finally
      // EndUpdate is always called, even if error occurred
      EndUpdate(e);
    end;
  end;
end;
```

## See Also

- [BeginUpdate](IwbElement_BeginUpdate.md)
