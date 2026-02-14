# wbRecordDefMap

## Syntax

```pascal
function wbRecordDefMap: IwbRecordDefMap;
```

## Description

Returns the record definition map interface, which provides access to all record type definitions used by the current game. This map contains the structural definitions for how each record signature is formatted and interpreted.

## Parameters

This function takes no parameters.

## Returns

Returns an IwbRecordDefMap interface providing access to record definitions.

## Example

```pascal
var
  defMap: IwbRecordDefMap;
begin
  defMap := wbRecordDefMap;

  if Assigned(defMap) then
    AddMessage('Record definition map is available');
end;
```

## See Also

- [GetRecordDefNames](Global_GetRecordDefNames.md)
