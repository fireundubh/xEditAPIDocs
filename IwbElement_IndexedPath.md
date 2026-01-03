# IndexedPath

## Syntax

```pascal
function IndexedPath(AElement: IwbElement; AIncludeMainRecord: Boolean): String;
```

## Description

Returns the indexed path of `AElement`. If `AIncludeMainRecord` is true, the path starts from the main record.

## Example

```pascal
AddMessage(IndexedPath(e, True));
```

## See Also

- [Path](IwbElement_Path.md)
- [FullPath](IwbElement_FullPath.md)
