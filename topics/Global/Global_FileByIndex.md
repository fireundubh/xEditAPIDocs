# FileByIndex

## Syntax

```pascal
function FileByIndex(AIndex: integer): IwbFile;
```

## Description

Returns the plugin at `AIndex` in the array of loaded files

## Example

```pascal
for i := 0 to Pred(FileCount) do
	f := FileByIndex(i);
```

## See Also

- [FileByLoadOrder - Global](Global_FileByLoadOrder.md)
- [FileByName - Global](Global_FileByName.md)
