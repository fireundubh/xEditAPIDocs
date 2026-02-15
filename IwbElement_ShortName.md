# ShortName

## Syntax

```pascal
function ShortName(AElement: IwbElement): string;
```

## Description

Returns a compact name representation optimized for display in limited space.

This function retrieves the ShortName property, which provides an abbreviated element identifier. The exact abbreviation strategy varies by element type but typically omits verbose prefixes or truncates long names. Useful for UI elements like tree views where space is limited. Returns an empty string for invalid elements. Generally shorter than Name but may be identical for simple elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose short name to retrieve |

## Returns

Returns a shortened version of the element's name as a string.

## Example

```pascal
// Example 1: Display compact element names in logs
var
  rec: IwbMainRecord;
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  short, full: string;
begin
  if Assigned(e) then begin
    container := e;
    AddMessage('Elements (short vs full):');
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        short := ShortName(element);
        full := Name(element);
        AddMessage(Format('  [%d] %s | %s', [i, short, full]));
      end;
    end;
  end;
end;

// Example 2: Build compact element tree
var
  rec: IwbMainRecord;
  conditions: IwbContainer;
  i: integer;
  condition, funcElement: IwbElement;
  shortName, funcValue: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      for i := 0 to ElementCount(conditions) - 1 do begin
        condition := ElementByIndex(conditions, i);
        if Assigned(condition) then begin
          shortName := ShortName(condition);
          funcElement := ElementByPath(condition, 'CTDA\Function');
          if Assigned(funcElement) then begin
            funcValue := GetEditValue(funcElement);
            AddMessage(Format('%s: %s', [shortName, funcValue]));
          end;
        end;
      end;
    end;
  end;
end;

// Example 3: Compare name variations
var
  rec: IwbMainRecord;
  element: IwbElement;
  short, base, display, full: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA\Value');
    if Assigned(element) then begin
      short := ShortName(element);
      base := BaseName(element);
      display := DisplayName(element);
      full := Name(element);
      AddMessage('Name variations:');
      AddMessage('  Short: ' + short);
      AddMessage('  Base: ' + base);
      AddMessage('  Display: ' + display);
      AddMessage('  Full: ' + full);
    end;
  end;
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [BaseName](IwbElement_BaseName.md)
- [DisplayName](IwbElement_DisplayName.md)
- [PathName](IwbElement_PathName.md)


