# ConflictThisForNode

## Syntax

```pascal
function ConflictThisForNode(AElement: IwbElement): TConflictThis;
```

## Description

Gets the specific conflict status for a node.

Returns a `TConflictThis` enumeration value representing the conflict state for the specified element itself, without considering child elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the specific conflict status for |

## Returns

Returns a TConflictThis enumeration value representing the conflict status.

## Example

```pascal
// Example 1: Check node-specific conflict
var
  element: IwbElement;
  conflictThis: TConflictThis;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'EDID');
    if Assigned(element) then begin
      conflictThis := ConflictThisForNode(element);
      AddMessage(Format('EDID node conflict: %d', [Ord(conflictThis)]));
    end;
  end;
end;

// Example 2: Compare ConflictThis vs ConflictAll
var
  element: IwbElement;
  conflictThis: TConflictThis;
  conflictAll: TConflictAll;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA');
    if Assigned(element) then begin
      conflictThis := ConflictThisForNode(element);
      conflictAll := ConflictAllForNode(element);
      AddMessage(Format('%s conflicts:', [Name(element)]));
      AddMessage(Format('  This node: %d', [Ord(conflictThis)]));
      AddMessage(Format('  Including children: %d', [Ord(conflictAll)]));
    end;
  end;
end;

// Example 3: Find elements with specific conflict
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  conflictThis: TConflictThis;
  matchCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    matchCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        conflictThis := ConflictThisForNode(element);
        // Look for specific conflict level (e.g., 2)
        if Ord(conflictThis) = 2 then begin
          Inc(matchCount);
          AddMessage(Format('Level 2 conflict: %s', [Name(element)]));
        end;
      end;
    end;

    AddMessage(Format('Found %d elements with level 2 conflict', [matchCount]));
  end;
end;
```

## See Also

- [ConflictAllForNode](IwbElement_ConflictAllForNode.md)


