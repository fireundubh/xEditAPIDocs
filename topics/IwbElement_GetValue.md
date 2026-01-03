# GetValue

## Syntax

```pascal
function GetValue(AElement: IwbElement): string;
```

## Description

Returns the string display value of an element as it is displayed in the UI. Useful for things like decoded texture hashes and such.

## Examples

```pascal
var
  value: string;
begin
  value := GetValue(element);
end;
```

## See Also

- [GetElementValues](IwbContainer_GetElementValues.md)


