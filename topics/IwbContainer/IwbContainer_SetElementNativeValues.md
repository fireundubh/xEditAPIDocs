# SetElementNativeValues

## Syntax

```pascal
procedure SetElementNativeValues(AContainer: IwbContainer; APath: string; AValue: Variant);
```

## Description

Changes the native value of an element in the container identified by the specified path.

This procedure modifies the internal native value of an element. The path parameter uses dot notation to navigate to nested elements. The value must match the native type expected by the target element.

## Examples

```pascal
var
  container: IwbContainer;
begin
  SetElementNativeValues(container, 'DATA\Weight', 10.5);
end
```

## See Also

- [SetElementEditValues](IwbContainer_SetElementEditValues.md)
