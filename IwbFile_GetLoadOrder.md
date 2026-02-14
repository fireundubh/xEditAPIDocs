# GetLoadOrder

## Syntax

```pascal
function GetLoadOrder(aeFile: IwbFile): integer;
```

## Description

Returns the load order index of a plugin file.

The function takes an IwbFile interface as input and returns its index in the load order. If the passed parameter is not a valid IwbFile interface, returns -1.

The load order index represents the position of the plugin in the overall load order, with master files typically having lower indices than dependent files.

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


