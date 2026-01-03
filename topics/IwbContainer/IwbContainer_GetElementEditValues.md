# GetElementEditValues

## Syntax

```pascal
function GetElementEditValues(AContainer: IwbContainer; APath: string): string;
```

## Description

Returns the edit value of an element in the container by path as a string. This is the value as it would appear in the editor.

## Examples

```pascal
var
  value: string;
begin
  value := GetElementEditValues(container, 'FULL'); // Get full name
end;
```

## See Also

- [GetElementNativeValues](IwbContainer_GetElementNativeValues.md)
