# GetLoadOrderFileID

## Syntax

```pascal
function GetLoadOrderFileID(AFile: IwbFile): String;
```

## Description

Returns the load order file ID of `AFile` as a string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose load order file ID to retrieve |

## Returns

Returns the load order file ID as a string.

## Example

```pascal
AddMessage(GetLoadOrderFileID(f));
```

## See Also

- [GetLoadOrder](IwbFile_GetLoadOrder.md)
