# GetLoadOrder

## Syntax

```pascal
function GetLoadOrder(AFile: IwbFile): Integer;
```

## Description

Returns the load-order index of `AFile`.

Index 0 is the first loaded file. The index is not a FormID module prefix. Use [GetLoadOrderFileID](IwbFile_GetLoadOrderFileID.md) for the slot string, and [FormID](IwbMainRecord_FormID.md) for a file FormID.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose load-order index is needed |

## Returns

The load-order index, or `-1` when `AFile` is not a file.

## Example

```pascal
var
  f: IwbFile;
  idx: Integer;
begin
  f := FileByIndex(0);
  if Assigned(f) then begin
    idx := GetLoadOrder(f);
    if idx = -1 then
      AddMessage('Not a file')
    else
      AddMessage('Load order index: ' + IntToStr(idx));
  end;
end;
```

## See Also

- [FileByLoadOrder](Global_FileByLoadOrder.md)
- [GetLoadOrderFileID](IwbFile_GetLoadOrderFileID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
