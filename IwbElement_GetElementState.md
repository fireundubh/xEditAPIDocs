# GetElementState

## Syntax

```pascal
function GetElementState(AElement: IwbElement; AState: TwbElementState): TwbElementState;
```

## Description

Checks the internal flags of an element.

This function is used to query the current state flags of an element. It's particularly useful for determining various conditions about the element's current state.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the state from |
| AState | TwbElementState | The state flag to check |

## Returns

Returns the element state as a TwbElementState enumeration value.

## Example

```pascal
// Example 1: Check if element has been modified
var
  rec: IwbMainRecord;
  element: IwbElement;
  state: TwbElementState;
begin
  if Assigned(e) then begin
    element := ElementByPath(rec, 'EDID');
    if Assigned(element) then begin
      state := GetElementState(element, esModified);
      if state = esModified then
        AddMessage(Format('%s EDID has been modified', [EditorID(rec)]))
      else
        AddMessage(Format('%s EDID is unmodified', [EditorID(rec)]));
    end;
  end;
end;

// Example 2: Track element state during processing
var
  rec: IwbMainRecord;
  valueElement: IwbElement;
  stateBefore, stateAfter: TwbElementState;
  oldValue: string;
begin
  if Assigned(e) then begin
    valueElement := ElementByPath(rec, 'DATA\Value');
    if Assigned(valueElement) then begin
      stateBefore := GetElementState(valueElement, esModified);
      oldValue := GetEditValue(valueElement);
      SetEditValue(valueElement, '100');
      stateAfter := GetElementState(valueElement, esModified);

      AddMessage(Format('Changed value from %s to 100', [oldValue]));
      AddMessage(Format('State before: %d, after: %d',
        [Ord(stateBefore), Ord(stateAfter)]));
    end;
  end;
end;

// Example 3: Check multiple element states
var
  rec: IwbMainRecord;
  element: IwbElement;
  modified, initialized, internal: TwbElementState;
begin
  if Assigned(e) then begin
    element := ElementByPath(rec, 'FULL');
    if Assigned(element) then begin
      modified := GetElementState(element, esModified);
      // Check other states as needed
      AddMessage(Format('Element %s states:', [Name(element)]));
      AddMessage(Format('  Modified: %d', [Ord(modified)]));
    end;
  end;
end;
```

## See Also

- [SetElementState](IwbElement_SetElementState.md)
- [ClearElementState](IwbElement_ClearElementState.md)


