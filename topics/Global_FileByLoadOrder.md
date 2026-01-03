# FileByLoadOrder

## Syntax

```pascal
function FileByLoadOrder(ALoadOrder: integer): IwbFile;
```

## Description

Returns the plugin at `ALoadOrder` in the array of loaded files

To pass a hexadecimal load order as an argument to this function, convert the string to an integer.

## Example

```pascal
sLoadOrderFromHexID := Copy(AHexFormID, 1, 2);
f := FileByLoadOrder(StrToInt('$' + sLoadOrderFromHexID));
r := RecordByFormID(f, StrToInt('$' + AHexFormID), True);
```

## See Also

- [FileByName](Global_FileByName.md)


