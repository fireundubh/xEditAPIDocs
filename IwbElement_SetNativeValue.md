# SetNativeValue

## Syntax

```pascal
procedure SetNativeValue(AElement: IwbElement; AValue: Variant);
```

## Description

Sets the element's value directly using its native data type.

This function assigns to the NativeValue property, which accepts a Variant containing the value in the appropriate type (integer, float, string, etc.). No string parsing or conversion is performed. The element must be editable and the Variant type must be compatible with the element's definition. This is more efficient than SetEditValue when you already have the value in its native type.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to set the value for |
| AValue | Variant | The new value in its native data type |

## Returns

This procedure does not return a value.

## Example

```pascal
// Example 1: Set integer value directly
var
  valueElement: IwbElement;
begin
  if Assigned(e) then begin
    valueElement := ElementByPath(e, 'DATA\Value');
    if Assigned(valueElement) then begin
      SetNativeValue(valueElement, 100); // Direct integer assignment
      AddMessage('Set value to 100');
    end;
  end;
end;

// Example 2: Set float value for precise calculations
var
  weightElement: IwbElement;
  newWeight: double;
begin
  if Assigned(e) then begin
    weightElement := ElementByPath(e, 'DATA\Weight');
    if Assigned(weightElement) then begin
      newWeight := 12.5;
      SetNativeValue(weightElement, newWeight);
      AddMessage(Format('Set weight to %.2f', [newWeight]));
    end;
  end;
end;

// Example 3: Batch update with native values (more efficient than EditValue)
var
  damageElement, speedElement, reachElement: IwbElement;
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      damageElement := ElementByPath(e, 'DATA\Damage');
      if Assigned(damageElement) then
        SetNativeValue(damageElement, 25);

      speedElement := ElementByPath(e, 'DATA\Speed');
      if Assigned(speedElement) then
        SetNativeValue(speedElement, 1.0);

      reachElement := ElementByPath(e, 'DATA\Reach');
      if Assigned(reachElement) then
        SetNativeValue(reachElement, 1.5);
    finally
      EndUpdate(e);
    end;
  end;
end;
```

## See Also

- [GetNativeValue](IwbElement_GetNativeValue.md)
- [SetEditValue](IwbElement_SetEditValue.md)
- [GetEditValue](IwbElement_GetEditValue.md)
- [SetElementNativeValues](IwbContainer_SetElementNativeValues.md)


