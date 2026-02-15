# EnumValues

## Syntax

```pascal
function EnumValues(AElement: IwbElement): string;
```

## Description

Retrieves the names of set enum values for an element.

For elements that represent a set of named enum values, this function returns a space-separated string containing all the names of values that are currently set.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get enum values from |

## Returns

Returns a space-separated string containing all the names of set enum values.

## Example

```pascal
// Example 1: Get enum values from element
var
  enumElement: IwbElement;
  enumValues: string;
begin
  if Assigned(e) then begin
    enumElement := ElementByPath(e, 'DNAM\Type');
    if Assigned(enumElement) then begin
      enumValues := EnumValues(enumElement);
      AddMessage(Format('Enum values: %s', [enumValues]));
      // Example output: "Type1 Type2 Type3"
    end;
  end;
end;

// Example 2: Parse enum values into list
var
  enumElement: IwbElement;
  enumString: string;
  valueList: TStringList;
  i: integer;
begin
  if Assigned(e) then begin
    enumElement := ElementByPath(e, 'Flags');
    if Assigned(enumElement) then begin
      enumString := EnumValues(enumElement);
      valueList := TStringList.Create;
      try
        valueList.Delimiter := ' ';
        valueList.StrictDelimiter := True;
        valueList.DelimitedText := enumString;

        AddMessage(Format('%d enum values:', [valueList.Count]));
        for i := 0 to valueList.Count - 1 do
          AddMessage(Format('  [%d] %s', [i, valueList[i]]));
      finally
        valueList.Free;
      end;
    end;
  end;
end;

// Example 3: Check for specific enum value
var
  typeElement: IwbElement;
  enumValues: string;
begin
  if Assigned(e) then begin
    typeElement := ElementByPath(e, 'DATA\Type');
    if Assigned(typeElement) then begin
      enumValues := EnumValues(typeElement);
      if Pos('Weapon', enumValues) > 0 then
        AddMessage(Format('%s type includes Weapon', [EditorID(e)]))
      else
        AddMessage(Format('%s type: %s', [EditorID(e), enumValues]));
    end;
  end;
end;
```

## See Also

- [SetEditValue](IwbElement_SetEditValue.md)


