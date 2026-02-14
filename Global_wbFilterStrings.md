# wbFilterStrings

## Syntax

```pascal
procedure wbFilterStrings(ASource: TStrings; ATarget: TStrings; AFilter: string);
```

## Description

Appends strings in `ASource` containing `AFilter`, ignoring case, to `ATarget`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ASource | TStrings | The source string list to filter |
| ATarget | TStrings | The target string list to append matches to |
| AFilter | string | The filter string to search for (case-insensitive) |

## Example

```pascal
wbFilterStrings(slAssets, slCloudTextures, sCloudTexturesLocation);
```

