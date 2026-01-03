# wbFilterStrings

## Syntax

```pascal
procedure wbFilterStrings(ASource: TStrings; ATarget: TStrings; AFilter: string);
```

## Description

Appends strings in `ASource` containing `AFilter`, ignoring case, to `ATarget`

## Example

```pascal
wbFilterStrings(slAssets, slCloudTextures, sCloudTexturesLocation);
```

