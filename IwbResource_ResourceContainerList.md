# ResourceContainerList

## Syntax

```pascal
procedure ResourceContainerList(AContainerPaths: TStrings);
```

## Description

Populates `AContainerPaths` with absolute paths to loaded resource containers

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerPaths | TStrings | The string list to populate with container paths |

## Example

```pascal
sl := TStringList.Create;
ResourceContainerList(sl);
```

