# ClearElementState

## Syntax

```pascal
procedure ClearElementState(AElement: IwbElement; AState: TwbElementState);
```

## Description

Manipulates the internal flags of an element.

This procedure allows you to clear specific state flags on elements. Common usage includes clearing the modified state of elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose state to clear |
| AState | TwbElementState | The state flag to clear |

## Element States

- `esModified`
- `esInternalModified`
- `esUnsaved`
- `esSortKeyValid`
- `esExtendedSortKeyValid`
- `esHidden`
- `esParentHidden`
- `esParentHiddenChecked`
- `esNotReachable`
- `esReachable`
- `esTagged`
- `esDeciding`
- `esResolving`
- `esNotSuitableToAddTo`

## Example

```pascal
// Example 1: Clear modified flag after inspection
var
  element: IwbElement;
  stateBefore: TwbElementState;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'EDID');
    if Assigned(element) then begin
      stateBefore := GetElementState(element, esModified);
      if stateBefore = esModified then begin
        ClearElementState(element, esModified);
        AddMessage(Format('Cleared modified state on EDID in %s', [EditorID(e)]));
      end;
    end;
  end;
end;

// Example 2: Reset modification tracking for batch operations
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  clearedCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    clearedCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        if GetElementState(element, esModified) = esModified then begin
          ClearElementState(element, esModified);
          Inc(clearedCount);
        end;
      end;
    end;

    AddMessage(Format('Cleared modified state on %d elements in %s',
      [clearedCount, EditorID(e)]));
  end;
end;

// Example 3: Conditional state clearing
var
  valueElement: IwbElement;
  currentValue: integer;
  isModified: TwbElementState;
begin
  if Assigned(e) then begin
    valueElement := ElementByPath(e, 'DATA\Value');
    if Assigned(valueElement) then begin
      currentValue := GetNativeValue(valueElement);
      isModified := GetElementState(valueElement, esModified);

      // Clear if value unchanged from default
      if (currentValue = 0) and (isModified = esModified) then begin
        ClearElementState(valueElement, esModified);
        AddMessage(Format('Cleared spurious modification flag in %s', [EditorID(e)]));
      end;
    end;
  end;
end;
```

## See Also

- [GetElementState](IwbElement_GetElementState.md)
- [SetElementState](IwbElement_SetElementState.md)


