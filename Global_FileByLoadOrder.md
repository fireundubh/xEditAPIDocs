# FileByLoadOrder

## Syntax

```pascal
function FileByLoadOrder(ALoadOrder: integer): IwbFile;
```

## Description

Returns the plugin at `ALoadOrder` in the array of loaded files

To pass a hexadecimal load order as an argument to this function, convert the string to an integer.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ALoadOrder | integer | The load order position of the file to retrieve |

## Returns

Returns the file at the specified load order position as an IwbFile interface.

## Example

```pascal
sLoadOrderFromHexID := Copy(AHexFormID, 1, 2);
f := FileByLoadOrder(StrToInt('$' + sLoadOrderFromHexID));
r := RecordByFormID(f, StrToInt('$' + AHexFormID), True);
```

## See Also

- [FileByName](Global_FileByName.md)


