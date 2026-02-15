# SetElementState

## Syntax

```pascal
function SetElementState(AElement: IwbElement; AState: TwbElementState): TwbElementState;
```

## Description

Modifies the internal state flags of an element.

Returns the previous state value before modification. Used to manipulate internal element states.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose state to modify |
| AState | TwbElementState | The new state to set |

## Returns

Returns the previous state value as a TwbElementState enumeration value.

## Example

```pascal
// Example 1: Mark element as modified
var
  rec: IwbMainRecord;
  element: IwbElement;
  previousState: TwbElementState;
begin
  if Assigned(e) then begin
    element := ElementByPath(rec, 'DATA\Value');
    if Assigned(element) then begin
      previousState := SetElementState(element, esModified);
      AddMessage(Format('Set element to modified, previous state: %d',
        [Ord(previousState)]));
    end;
  end;
end;

// Example 2: Save and restore element state
var
  rec: IwbMainRecord;
  element: IwbElement;
  savedState, currentState: TwbElementState;
begin
  if Assigned(e) then begin
    element := ElementByPath(rec, 'EDID');
    if Assigned(element) then begin
      // Save current state
      savedState := GetElementState(element, esModified);

      // Do work that might change state
      SetEditValue(element, 'TempValue');

      // Restore previous state if needed
      currentState := SetElementState(element, savedState);
      AddMessage(Format('Restored state from %d to %d',
        [Ord(currentState), Ord(savedState)]));
    end;
  end;
end;

// Example 3: Batch state modification with error handling
var
  rec: IwbMainRecord;
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  previousState: TwbElementState;
  stateCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    stateCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) and (ElementType(element) = etValue) then begin
        try
          previousState := SetElementState(element, esModified);
          Inc(stateCount);
        except
          on E: Exception do
            AddMessage(Format('Failed to set state on %s: %s',
              [Name(element), E.Message]));
        end;
      end;
    end;

    AddMessage(Format('Modified state on %d elements', [stateCount]));
  end;
end;
```

## See Also

- [GetElementState](IwbElement_GetElementState.md)
- [ClearElementState](IwbElement_ClearElementState.md)
- [IsEditable](IwbElement_IsEditable.md)


