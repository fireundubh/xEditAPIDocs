# GetElementNativeValues

## Syntax

```pascal
function GetElementNativeValues(AContainer: IwbContainer; APath: string): Variant;
```

## Description

Returns the native value of an element in the container by path. The return type is `Variant` to accommodate different value types.

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


