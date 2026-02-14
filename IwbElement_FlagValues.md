# FlagValues

## Syntax

```pascal
function FlagValues(AElement: IwbElement): string;
```

## Description

Returns the names of all set flags for an element.

For elements that represent a set of flags, this function returns the names of all set flags, separated with spaces.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get flag values from |

## Returns

Returns a space-separated string containing the names of all set flags.

## Example

```pascal
var
  element: IwbElement;
  flags: string;
begin
  flags := FlagValues(element);
  // flags might contain something like "Flag1 Flag2 Flag3"
end;
```

## See Also

- [EnumValues](IwbElement_EnumValues.md)


