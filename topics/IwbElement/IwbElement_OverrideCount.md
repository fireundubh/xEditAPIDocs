# OverrideCount (IwbElement)

## Syntax

```pascal
function OverrideCount(AElement: IwbElement): integer;
```

## Description

Returns the number of override records for this element.

For master records, this function returns the number of override records that exist in other plugins. Returns 0 for elements that are not master records.

## Example

```pascal
var
  element: IwbElement;
  count: integer;
begin
  count := OverrideCount(element);
  if count > 0 then
    // Handle elements with overrides
end;
```

## See Also

- [IsWinningOverride](../IwbMainRecord/IwbMainRecord_IsWinningOverride.md)
- [IsMaster](../IwbMainRecord/IwbMainRecord_IsMaster.md)
