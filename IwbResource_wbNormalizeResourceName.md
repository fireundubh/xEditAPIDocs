# wbNormalizeResourceName

## Syntax

```pascal
function wbNormalizeResourceName(AResourceName: string; AAssetType: integer): string;
```

## Description

Finds a known asset root in a path and returns the path from that root. The search treats `/` and `\` as the same and ignores letter case. The result keeps the letters of the original path, converts slashes to backslashes, and collapses a doubled backslash. A name shorter than two characters, or a name that contains `#8` followed by `NOR`, returns an empty string.

When the path has no known root, the root for `AAssetType` is added in front. A rooted path keeps only the file name. `atNone` (`0`) picks the root from the extension. Voice and music are treated as sound, and an extension that matches nothing is treated as a mesh.

`AAssetType` is a `TwbAssetType` value. Use an `at*` constant such as `atTexture`. `resTexture` is the same value as `atTexture`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AResourceName | string | Path or filename to search |
| AAssetType | integer | `TwbAssetType` value, used when the path has no known root |

## Returns

The path from the asset root, or an empty string when the name is shorter than two characters.

## Example

```pascal
var
  texturePath: string;
  normalizedPath: string;
begin
  texturePath := 'Textures/Armor/Iron/IronArmor_d.DDS';
  normalizedPath := wbNormalizeResourceName(texturePath, atTexture);
  AddMessage(normalizedPath);
end;
```

## See Also

- [ResourceExists](IwbResource_ResourceExists.md)
