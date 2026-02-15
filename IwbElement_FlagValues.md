# FlagValues

## Syntax

```pascal
function FlagValues(AElement: IwbElement): string;
```

## Description

Returns the names of all set flags for an element.

For elements that represent a set of flags, this function returns the names of all set flags, separated with spaces.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get flag values from |

## Returns

Returns a space-separated string containing the names of all set flags.

## Example

```pascal
// Example 1: Get set flags from element
var
  flagElement: IwbElement;
  setFlags: string;
begin
  if Assigned(e) then begin
    flagElement := ElementByPath(e, 'Record Flags');
    if Assigned(flagElement) then begin
      setFlags := FlagValues(flagElement);
      AddMessage(Format('%s flags: %s', [EditorID(e), setFlags]));
      // Example output: "ESM Compressed"
    end;
  end;
end;

// Example 2: Check for specific flag
var
  flagElement: IwbElement;
  flagString: string;
begin
  if Assigned(e) then begin
    flagElement := ElementByPath(e, 'ACBS\Flags');
    if Assigned(flagElement) then begin
      flagString := FlagValues(flagElement);
      if Pos('Essential', flagString) > 0 then
        AddMessage(Format('%s is marked Essential', [EditorID(e)]))
      else
        AddMessage(Format('%s flags: %s', [EditorID(e), flagString]));
    end;
  end;
end;

// Example 3: Parse and count flags
var
  flagElement: IwbElement;
  flagString: string;
  flagList: TStringList;
  i: integer;
begin
  if Assigned(e) then begin
    flagElement := ElementByPath(e, 'DATA\Flags');
    if Assigned(flagElement) then begin
      flagString := FlagValues(flagElement);
      flagList := TStringList.Create;
      try
        flagList.Delimiter := ' ';
        flagList.StrictDelimiter := True;
        flagList.DelimitedText := flagString;

        AddMessage(Format('%s has %d flags set:', [EditorID(e), flagList.Count]));
        for i := 0 to flagList.Count - 1 do
          AddMessage(Format('  - %s', [flagList[i]]));
      finally
        flagList.Free;
      end;
    end;
  end;
end;
```

## See Also

- [EnumValues](IwbElement_EnumValues.md)


