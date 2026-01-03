# GetLoadOrder

## Syntax

```pascal
function GetLoadOrder(aeFile: IwbFile): integer;
```

## Description

Returns the load order index of a plugin file.

The function takes an IwbFile interface as input and returns its index in the load order. If the passed parameter is not a valid IwbFile interface, returns -1.

The load order index represents the position of the plugin in the overall load order, with master files typically having lower indices than dependent files.

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

- [FileByLoadOrder](../Global/Global_FileByLoadOrder.md)
- [GetLoadOrderFormID](../IwbMainRecord/IwbMainRecord_GetLoadOrderFormID.md)
