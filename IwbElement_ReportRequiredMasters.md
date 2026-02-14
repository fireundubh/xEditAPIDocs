# ReportRequiredMasters

## Syntax

```pascal
procedure ReportRequiredMasters(AElement: IwbElement; AListOut: TStrings; AAsNew: boolean; ARecursive: boolean);
```

## Description

Checks which master files an element depends on and adds their filenames to the output list.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check for required masters |
| AListOut | TStrings | The string list to store the required master filenames |
| AAsNew | boolean | Boolean parameter for checking as new |
| ARecursive | boolean | If true, checks children elements of containers |

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

- [HasMaster](IwbFile_HasMaster.md)
- [IsMaster](IwbMainRecord_IsMaster.md)
- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)


