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

## Examples

```pascal
var
  value: Variant;
begin
  value := GetElementNativeValues(container, 'DATA\Weight');
end;
```

## See Also

- [GetElementEditValues](IwbContainer_GetElementEditValues.md)


