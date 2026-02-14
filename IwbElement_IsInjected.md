# IsInjected

## Syntax

```pascal
function IsInjected(AElement: IwbElement): boolean;
```

## Description

Checks whether the element was created programmatically rather than loaded from disk.

This function retrieves the IsInjected property, which returns true if the element was created at runtime by scripts, xEdit operations, or other programmatic means, rather than being read from the plugin file. Injected elements exist only in memory until the file is saved. Returns false for elements loaded from disk or invalid inputs. Useful for distinguishing between original and runtime-created content.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check if it was injected |

## Returns

Returns true if the element was injected by another plugin, false otherwise.

## Example

```pascal
var
  element: IwbElement;
begin
  if IsInjected(element) then
    // Handle injected element
end;
```

## See Also

- [IsMaster](IwbMainRecord_IsMaster.md)
- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)


