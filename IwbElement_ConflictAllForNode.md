# ConflictAllForNode

## Syntax

```pascal
function ConflictAllForNode(AElement: IwbElement): TConflictAll;
```

## Description

Gets the overall conflict status for a node and its children.

Returns a `TConflictAll` enumeration value representing the conflict state for the specified element and all its child elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the overall conflict status for |

## Returns

Returns a TConflictAll enumeration value representing the conflict status.

## Example

```pascal
// Example 1: Check element conflict status
var
  element: IwbElement;
  conflictAll: TConflictAll;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA');
    if Assigned(element) then begin
      conflictAll := ConflictAllForNode(element);
      AddMessage(Format('DATA conflict level: %d', [Ord(conflictAll)]));
    end;
  end;
end;

// Example 2: Find conflicting elements
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  conflictAll: TConflictAll;
  conflictCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    conflictCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        conflictAll := ConflictAllForNode(element);
        if Ord(conflictAll) > 0 then begin
          Inc(conflictCount);
          AddMessage(Format('Conflict in %s: level %d',
            [Name(element), Ord(conflictAll)]));
        end;
      end;
    end;

    AddMessage(Format('%d conflicting elements found', [conflictCount]));
  end;
end;

// Example 3: Categorize conflict severity
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  conflictAll: TConflictAll;
  minor, major, critical: integer;
begin
  if Assigned(e) then begin
    container := e;
    minor := 0;
    major := 0;
    critical := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        conflictAll := ConflictAllForNode(element);
        case Ord(conflictAll) of
          1..2: Inc(minor);
          3..4: Inc(major);
          5..10: Inc(critical);
        end;
      end;
    end;

    AddMessage(Format('Conflicts: %d minor, %d major, %d critical',
      [minor, major, critical]));
  end;
end;
```

## See Also

- [ConflictThisForNode](IwbElement_ConflictThisForNode.md)


