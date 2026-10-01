# FileByLoadOrder

## Syntax

```pascal
function FileByLoadOrder(ALoadOrder: integer): IwbFile;
```

## Description

Returns the loaded file whose load order equals `ALoadOrder`.

`ALoadOrder` must be a number, and it must be less than the number of loaded files. Otherwise the call raises an invalid-argument error. A negative number does not raise. It returns nil, because no file has that load order. A number inside that range also returns nil when no loaded file uses it as its load order.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ALoadOrder | integer | Load order to find. Must be less than the number of loaded files |

## Returns

The `IwbFile` with that load order, or nil when none has it.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByLoadOrder(0);
  if Assigned(f) then
    AddMessage(GetFileName(f));
end;
```

## See Also

- [FileByIndex](Global_FileByIndex.md)
- [FileByName](Global_FileByName.md)
- [FileCount](Global_FileCount.md)
