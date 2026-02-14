# IndexedPath

## Syntax

```pascal
function IndexedPath(AElement: IwbElement; AIncludeMainRecord: Boolean): String;
```

## Description

Returns the indexed path of `AElement`. If `AIncludeMainRecord` is true, the path starts from the main record.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the indexed path from |
| AIncludeMainRecord | Boolean | Whether to include the main record in the path |

## Returns

Returns the indexed path as a string.

## Example

```pascal
AddMessage(IndexedPath(e, True));
```

## See Also

- [Path](IwbElement_Path.md)
- [FullPath](IwbElement_FullPath.md)
- [PathName](IwbElement_PathName.md)
- [Name](IwbElement_Name.md)
