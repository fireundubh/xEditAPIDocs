# ResourceContainerList

## Syntax

```pascal
procedure ResourceContainerList(AContainerPaths: TStrings);
```

## Description

Populates `AContainerPaths` with absolute paths to loaded resource containers

## Example

```pascal
sl := TStringList.Create;
ResourceContainerList(sl);
```
