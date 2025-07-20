# FileByName

## Syntax

```pascal
function FileByName(AFileName: string): IwbFile;
```

## Description

Returns the plugin named `AFileName` from the array of loaded files, or `nil` if the file cannot be found

If this routine is not available in your version of xEdit, you can duplicate the function like so:

```pascal
function FileByName(AFileName: string): IwbFile;
var
	f : IwbFile;
	i : integer;
begin
  Result := nil;

  for i := 0 to Pred(FileCount) do
  begin
    f := FileByIndex(i);

    if SameText(AFileName, GetFileName(f)) then
    begin
      Result := f;
      Break;
    end;
  end;
end;
```

## Example

```pascal
f := FileByName('Skyrim.esm');

if not Assigned(f) then
	Exit;

r := RecordByIndex(f, 0);   // --> DoorMarker [STAT:00000001]
```

## See Also

- [FileByIndex - Global](Global_FileByIndex.md)
- [FileByLoadOrder - Global](Global_FileByLoadOrder.md)
