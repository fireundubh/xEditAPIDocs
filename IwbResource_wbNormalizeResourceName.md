# wbNormalizeResourceName

## Syntax

```pascal
function wbNormalizeResourceName(aResourceName: string; aResourceType: TGameResourceType): string;
```

## Description

Normalizes a resource name according to game-specific conventions. This function adjusts path separators, case, and format to match the expected resource naming standards for the current game.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aResourceName | string | The resource name to normalize |
| aResourceType | TGameResourceType | The type of resource (resMesh, resTexture, resSound, resMusic, resMaterial) |

## Returns

Returns a string containing the normalized resource name.

## Example

```pascal
var
  texturePath: string;
  normalizedPath: string;
begin
  texturePath := 'Textures/Armor/Iron/IronArmor_d.DDS';
  normalizedPath := wbNormalizeResourceName(texturePath, resTexture);

  AddMessage('Normalized path: ' + normalizedPath);
  // Output: textures\armor\iron\ironarmor_d.dds
end;
```

## See Also

- [ResourceExists](IwbContainer_ResourceExists.md)
