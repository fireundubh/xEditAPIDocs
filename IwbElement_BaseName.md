# BaseName

## Syntax

```pascal
function BaseName(AElement: IwbElement): string;
```

## Description

Returns the base name of an element without load order index prefixes.

This function is identical to `Name` except for how it handles IwbFiles. While `Name` will prepend a load order index (i.e. [02] PluginName.esp), `BaseName` will not include this prefix.

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


