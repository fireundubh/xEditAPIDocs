# GetLoadOrder

## Syntax

```pascal
function GetLoadOrder(aeFile: IwbFile): integer;
```

## Description

Returns the zero-based load order position of the plugin file.

This function retrieves the LoadOrder property, which indicates the file's position in the current plugin load order. Index 0 is the first file loaded (typically the main game master). The load order determines file priority and FormID resolution. Returns -1 for invalid file references. Note that load order can change between sessions if the plugin list is modified.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aeFile | IwbFile | The file to get the load order index from |

## Returns

Returns the load order index of the file, or -1 if the parameter is not a valid IwbFile.

## Example

```pascal
var
    f: IwbFile;
    idx: integer;
begin
    f := // ... get file reference
    idx := GetLoadOrder(f);
    if idx = -1 then
        AddMessage('Not a valid file')
    else
        AddMessage('Load order index: ' + IntToStr(idx));
end;
```

## See Also

- [FileByLoadOrder](Global_FileByLoadOrder.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)


