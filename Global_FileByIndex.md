# FileByIndex

## Syntax

```pascal
function FileByIndex(AIndex: integer): IwbFile;
```

## Description

Returns the plugin at `AIndex` in the array of loaded files

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AIndex | integer | The zero-based index of the file in the loaded files array |

## Returns

Returns the file at the specified index as an IwbFile interface.

## Example

```pascal
for i := 0 to Pred(FileCount) do
	f := FileByIndex(i);
```

## See Also

- [FileByLoadOrder](Global_FileByLoadOrder.md)
- [FileByName](Global_FileByName.md)


