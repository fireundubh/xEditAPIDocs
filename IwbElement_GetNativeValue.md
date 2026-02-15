# GetNativeValue

## Syntax

```pascal
function GetNativeValue(AElement: IwbElement): Variant;
```

## Description

Returns the element's value in its native data type as a Variant.

This function retrieves the NativeValue property, which returns the element's internal value without string formatting. The Variant type depends on the element definition (e.g., integers for numeric fields, floats for real numbers, strings for text). Returns an empty string (as Variant) if the element is invalid. Prefer this over GetEditValue for programmatic comparisons and calculations.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the native value from |

## Returns

Returns the element's native value as a Variant type.

## Example

```pascal
// Example 1: Get numeric value for calculations
var
  weightElement: IwbElement;
  weight: Variant;
  newWeight: double;
begin
  if Assigned(e) then begin
    weightElement := ElementByPath(e, 'DATA\Weight');
    if Assigned(weightElement) then begin
      weight := GetNativeValue(weightElement);
      newWeight := weight * 0.5; // Halve the weight
      SetNativeValue(weightElement, newWeight);
      AddMessage(Format('Reduced weight from %.2f to %.2f', [weight, newWeight]));
    end;
  end;
end;

// Example 2: Type-safe value retrieval
var
  valueElement: IwbElement;
  value: Variant;
  intValue: integer;
begin
  if Assigned(e) then begin
    valueElement := ElementByPath(e, 'DATA\Value');
    if Assigned(valueElement) then begin
      value := GetNativeValue(valueElement);
      if VarType(value) = varInteger then begin
        intValue := value;
        if intValue < 10 then
          AddMessage('Low value item: ' + IntToStr(intValue));
      end;
    end;
  end;
end;

// Example 3: Compare values programmatically
var
  rec2: IwbMainRecord;
  value1, value2: Variant;
begin
  if Assigned(e) then begin
    rec2 := WinningOverride(e);

    if Assigned(rec2) then begin
      value1 := GetNativeValue(ElementByPath(e, 'DATA\Damage'));
      value2 := GetNativeValue(ElementByPath(rec2, 'DATA\Damage'));

      if value1 <> value2 then
        AddMessage(Format('Damage changed from %s to %s', [VarToStr(value1), VarToStr(value2)]));
    end;
  end;
end;
```

## See Also

- [SetNativeValue](IwbElement_SetNativeValue.md)
- [GetEditValue](IwbElement_GetEditValue.md)
- [SetEditValue](IwbElement_SetEditValue.md)
- [GetValue](IwbElement_GetValue.md)
- [GetElementNativeValues](IwbContainer_GetElementNativeValues.md)


