# CanContainFormIDs

## Syntax

```pascal
function CanContainFormIDs(AElement: IwbElement): boolean;
```

## Description

Checks whether the element's definition allows it to contain FormID references.

This function retrieves the CanContainFormIDs property, which returns true if the element's structure can include FormID fields (either directly or in descendant elements). This is an optimization hint used by BuildRef to skip branches that cannot contain references. Returns false for simple value types (integers, strings, etc.) but may return false negatively (false when it actually can). Returns false for invalid elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check |

## Returns

Returns `true` if the element can contain form IDs. Note that a `false` result is not guaranteed to mean the element cannot contain form IDs.

## Example

```pascal
// Example 1: Check if element can contain FormIDs
var
  element: IwbElement;
  canContain: boolean;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'KWDA');
    if Assigned(element) then begin
      canContain := CanContainFormIDs(element);
      if canContain then
        AddMessage('KWDA can contain FormIDs')
      else
        AddMessage('KWDA cannot contain FormIDs');
    end;
  end;
end;

// Example 2: Optimize FormID processing
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  processedCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    processedCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        // Skip elements that cannot contain FormIDs
        if CanContainFormIDs(element) then begin
          BuildRef(element);
          Inc(processedCount);
        end;
      end;
    end;

    AddMessage(Format('Processed %d elements for FormID references', [processedCount]));
  end;
end;

// Example 3: Categorize elements by FormID capability
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  canContainCount, cannotContainCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    canContainCount := 0;
    cannotContainCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        if CanContainFormIDs(element) then
          Inc(canContainCount)
        else
          Inc(cannotContainCount);
      end;
    end;

    AddMessage(Format('%s element analysis:', [EditorID(e)]));
    AddMessage(Format('  Can contain FormIDs: %d', [canContainCount]));
    AddMessage(Format('  Cannot contain FormIDs: %d', [cannotContainCount]));
  end;
end;
```

## See Also

- [LinksTo](IwbElement_LinksTo.md)
- [BuildRef](IwbElement_BuildRef.md)
- [FormID](IwbMainRecord_FormID.md)


