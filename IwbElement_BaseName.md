# BaseName

## Syntax

```pascal
function BaseName(AElement: IwbElement): string;
```

## Description

Returns the element's name without load order prefixes or other decorations.

This function retrieves the BaseName property, which provides the undecorated element identifier. For files, this returns just the filename without the load order index prefix (e.g., "Plugin.esp" instead of "[02] Plugin.esp"). For other elements, behavior is similar to Name. Useful when you need the clean identifier for comparisons or when building user-facing strings. Returns an empty string for invalid elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose base name to retrieve |

## Returns

Returns the base name of the element as a string, without load order prefixes for file elements.

## Example

```pascal
var
  element: IwbElement;
  baseName: string;
begin
  baseName := BaseName(element); // Returns "PluginName.esp" instead of "[02] PluginName.esp"
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [DisplayName](IwbElement_DisplayName.md)
- [ShortName](IwbElement_ShortName.md)


