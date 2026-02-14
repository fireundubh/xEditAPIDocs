# wbRemoveDuplicateStrings

## Syntax

```pascal
procedure wbRemoveDuplicateStrings(AList: TStringList);
```

## Description

Removes duplicate strings from `AList`, modifying the list in-place

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AList | TStringList | The string list to remove duplicates from |

## Example

```pascal
slAssets.Sort;
wbRemoveDuplicateStrings(slAssets);
```

