# GetMasters

## Syntax

```pascal
procedure GetMasters(AFile: IwbFile; AFileNames: TStrings);
```

## Description

Appends the master file names of `AFile` to `AFileNames`.

The list is not cleared first. Clear it if you want only this file's masters. The names are in master-list order.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to read masters from |
| AFileNames | TStrings | The list that receives the names |

## Returns

Returns nothing.

## Example

```pascal
var
  f: IwbFile;
  masters: TStringList;
  i: Integer;
begin
  f := FileByIndex(0);
  if Assigned(f) then begin
    masters := TStringList.Create;
    try
      GetMasters(f, masters);
      for i := 0 to Pred(masters.Count) do
        AddMessage(masters.Strings[i]);
    finally
      masters.Free;
    end;
  end;
end;
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [AddMasters](IwbFile_AddMasters.md)
- [MasterByIndex](IwbFile_MasterByIndex.md)
- [MasterCount](IwbFile_MasterCount.md)
