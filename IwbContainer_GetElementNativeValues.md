# GetElementNativeValues

## Syntax

```pascal
function GetElementNativeValues(AContainer: IwbContainer; APath: string): Variant;
```

## Description

Returns the native value of an element in the container by path. The return type is `Variant` to accommodate different value types.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve the value from |
| APath | string | The element path to the value |

## Returns

Returns the native value as a Variant type.

## Example

```pascal
// Example 1: Read numeric values with correct type
var
  valueInt: integer;
  weightFloat: double;
  healthInt: integer;
begin
  if Assigned(e) then begin
    valueInt := GetElementNativeValues(e, 'DATA\Value');
    weightFloat := GetElementNativeValues(e, 'DATA\Weight');
    healthInt := GetElementNativeValues(e, 'DATA\Health');

    AddMessage(Format('Value: %d (int)', [valueInt]));
    AddMessage(Format('Weight: %.2f (float)', [weightFloat]));
    AddMessage(Format('Health: %d (int)', [healthInt]));
  end;
end;

// Example 2: Perform calculations with native values
var
  value, weight: double;
  valuePerPound: double;
begin
  if Assigned(e) then begin
    value := GetElementNativeValues(e, 'DATA\Value');
    weight := GetElementNativeValues(e, 'DATA\Weight');

    if weight > 0 then begin
      valuePerPound := value / weight;
      AddMessage(Format('Value per pound: %.2f', [valuePerPound]));
    end else
      AddMessage('Item has no weight');
  end;
end;

// Example 3: Read FormID as integer
var
  keywordFormID: integer;
  keywordHex: string;
begin
  if Assigned(e) then begin
    keywordFormID := GetElementNativeValues(e, 'KWDA\[0]');
    if keywordFormID <> 0 then begin
      keywordHex := IntToHex(keywordFormID, 8);
      AddMessage(Format('First keyword FormID: %d (0x%s)', [keywordFormID, keywordHex]));
    end;
  end;
end;

// Example 4: Compare native vs edit values
var
  nativeValue: Variant;
  editValue: string;
  weight: double;
begin
  if Assigned(e) then begin
    // Native value is a number
    nativeValue := GetElementNativeValues(e, 'DATA\Weight');
    weight := nativeValue;

    // Edit value is a formatted string
    editValue := GetElementEditValues(e, 'DATA\Weight');

    AddMessage(Format('Native: %.6f, Edit: %s', [weight, editValue]));
  end;
end;
```

## See Also

- [SetElementNativeValues](IwbContainer_SetElementNativeValues.md)
- [GetElementEditValues](IwbContainer_GetElementEditValues.md)
- [GetNativeValue](IwbElement_GetNativeValue.md)


