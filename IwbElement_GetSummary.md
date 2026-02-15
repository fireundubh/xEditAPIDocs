# GetSummary

## Syntax

```pascal
function GetSummary(AElement: IwbElement): String;
```

## Description

Returns a summary string for `AElement`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get a summary for |

## Returns

Returns a summary string describing the element.

## Example

```pascal
// Example 1: Get element summary for logging
var
  element: IwbElement;
  summary: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'EDID');
    if Assigned(element) then begin
      summary := GetSummary(element);
      AddMessage(Format('EDID summary: %s', [summary]));
    end;
  end;
end;

// Example 2: Build overview of record contents
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  name, summary: string;
begin
  if Assigned(e) then begin
    container := e;
    AddMessage(Format('Summary of %s:', [EditorID(e)]));
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        name := Name(element);
        summary := GetSummary(element);
        if summary <> '' then
          AddMessage(Format('  %s: %s', [name, summary]))
        else
          AddMessage(Format('  %s: (no summary)', [name]));
      end;
    end;
  end;
end;

// Example 3: Quick record inspection
var
  recSummary: string;
  edidSummary, fullSummary: string;
  edid, full: IwbElement;
begin
  if Assigned(e) then begin
    recSummary := GetSummary(e);
    AddMessage(Format('Record summary: %s', [recSummary]));

    edid := ElementByPath(e, 'EDID');
    full := ElementByPath(e, 'FULL');

    if Assigned(edid) then begin
      edidSummary := GetSummary(edid);
      AddMessage(Format('  EDID: %s', [edidSummary]));
    end;

    if Assigned(full) then begin
      fullSummary := GetSummary(full);
      AddMessage(Format('  FULL: %s', [fullSummary]));
    end;
  end;
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [DisplayName](IwbElement_DisplayName.md)
- [GetValue](IwbElement_GetValue.md)
