# Assigned

## Syntax

```pascal
function Assigned(AElement: IwbElement): boolean;
```

## Description

Checks if an xEdit element reference is valid.

This is an overloaded version of Delphi's native `Assigned` function, specifically for `IwbElement` interfaces. Returns `true` if the element reference is not nil, `false` otherwise.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check for validity |

## Returns

Returns `true` if the element reference is not nil, `false` otherwise.

## Example

```pascal
// Example 1: Safe element access
var
  rec: IwbMainRecord;
  edidElement: IwbElement;
  edid: string;
begin
  rec := e;
  if Assigned(rec) then begin
    edidElement := ElementByPath(rec, 'EDID');
    if Assigned(edidElement) then begin
      edid := GetEditValue(edidElement);
      AddMessage('Editor ID: ' + edid);
    end else
      AddMessage('No EDID element found');
  end;
end;

// Example 2: Verify reference resolution
var
  rec: IwbMainRecord;
  baseElement: IwbElement;
  baseRecord: IwbMainRecord;
begin
  rec := e;
  if Assigned(rec) then begin
    baseElement := ElementByPath(rec, 'NAME');
    if Assigned(baseElement) then begin
      baseRecord := LinksTo(baseElement);
      if Assigned(baseRecord) then
        AddMessage(Format('%s references %s', [EditorID(rec), EditorID(baseRecord)]))
      else
        AddMessage(Format('%s has invalid base reference', [EditorID(rec)]));
    end;
  end;
end;

// Example 3: Defensive iteration over optional elements
var
  rec: IwbMainRecord;
  keywords: IwbContainer;
  i: integer;
  kwdElement: IwbElement;
begin
  rec := e;
  if Assigned(rec) then begin
    keywords := ElementByPath(rec, 'KWDA');
    if Assigned(keywords) then begin
      for i := 0 to ElementCount(keywords) - 1 do begin
        kwdElement := ElementByIndex(keywords, i);
        // Always check before using element
        if Assigned(kwdElement) then
          AddMessage(Format('Keyword %d: %s', [i, GetEditValue(kwdElement)]))
        else
          AddMessage(Format('Keyword %d is nil (should not happen)', [i]));
      end;
    end else
      AddMessage(Format('%s has no keywords', [EditorID(rec)]));
  end;
end;
```

## See Also

- [Check](IwbElement_Check.md)


