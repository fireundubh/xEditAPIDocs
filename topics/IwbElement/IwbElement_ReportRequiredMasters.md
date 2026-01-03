# ReportRequiredMasters

## Syntax

```pascal
procedure ReportRequiredMasters(AElement: IwbElement; AListOut: TStrings; AAsNew: boolean; ARecursive: boolean);
```

## Description

Checks which master files an element depends on and adds their filenames to the output list.

### Arguments

- `AElement`: The element to check
- `AListOut`: List to store the required master filenames
- `AAsNew`: Boolean parameter for checking as new
- `ARecursive`: If true, checks children elements of containers

## Example

```pascal
var
    masters: TStringList;
begin
    masters := TStringList.Create;
    try
        ReportRequiredMasters(element, masters, False, True);
    finally
        masters.Free;
    end;
end;
```

## See Also

- [HasMaster](../IwbFile/IwbFile_HasMaster.md)
- [IsMaster](../IwbMainRecord/IwbMainRecord_IsMaster.md)
- [Master](../IwbMainRecord/IwbMainRecord_Master.md)
- [MasterOrSelf](../IwbMainRecord/IwbMainRecord_MasterOrSelf.md)
