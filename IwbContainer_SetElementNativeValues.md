# SetElementNativeValues

## Syntax

```pascal
procedure SetElementNativeValues(AContainer: IwbContainer; APath: string; AValue: Variant);
```

## Description

Changes the native value of an element in the container identified by the specified path.

This procedure modifies the internal native value of an element. The path parameter uses dot notation to navigate to nested elements. The value must match the native type expected by the target element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container containing the element to modify |
| APath | string | The element path to the value |
| AValue | Variant | The new native value to set |

## Example

```pascal
// Example 1: Update numeric values with correct types
var
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      SetElementNativeValues(e, 'DATA\Value', 500);        // Integer
      SetElementNativeValues(e, 'DATA\Weight', 12.5);      // Float
      SetElementNativeValues(e, 'DATA\Health', 100);       // Integer
      AddMessage('Updated DATA fields with native values');
    finally
      EndUpdate(e);
    end;
  end;
end;

// Example 2: Perform calculations and set result
var
  currentValue, currentWeight: double;
  newValue: double;
begin
  if Assigned(e) then begin
    currentValue := GetElementNativeValues(e, 'DATA\Value');
    currentWeight := GetElementNativeValues(e, 'DATA\Weight');

    // Double the value
    newValue := currentValue * 2;

    SetElementNativeValues(e, 'DATA\Value', Round(newValue));
    AddMessage(Format('Updated value from %d to %d', [Round(currentValue), Round(newValue)]));
  end;
end;

// Example 3: Set FormID as integer
var
  keywordFormID: integer;
begin
  if Assigned(e) then begin
    keywordFormID := $00012345;  // FormID as hex integer
    SetElementNativeValues(e, 'KWDA\[0]', keywordFormID);
    AddMessage(Format('Set keyword FormID to 0x%s', [IntToHex(keywordFormID, 8)]));
  end;
end;

// Example 4: Batch update with native types for performance
var
  i: integer;
  conditions: IwbContainer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      BeginUpdate(conditions);
      try
        // Update all condition comparison values
        for i := 0 to ElementCount(conditions) - 1 do begin
          SetElementNativeValues(e,
            Format('Conditions\[%d]\CTDA\Comparison Value', [i]),
            i + 1);  // Set to 1, 2, 3, etc.
        end;
        AddMessage(Format('Updated %d condition values', [ElementCount(conditions)]));
      finally
        EndUpdate(conditions);
      end;
    end;
  end;
end;
```

## See Also

- [GetElementNativeValues](IwbContainer_GetElementNativeValues.md)
- [SetElementEditValues](IwbContainer_SetElementEditValues.md)
- [SetNativeValue](IwbElement_SetNativeValue.md)


