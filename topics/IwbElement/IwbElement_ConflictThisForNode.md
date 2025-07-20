# ConflictThisForNode

## Syntax

```pascal
function ConflictThisForNode(AElement: IwbElement): TConflictThis;
```

## Description

Gets the specific conflict status for a node.

Returns a `TConflictThis` enumeration value representing the conflict state for the specified element itself, without considering child elements.

## Example

```pascal
var
  conflict: TConflictThis;
begin
  conflict := ConflictThisForNode(someElement);
end;
```

## See Also

- [ConflictAllForNode - IwbElement](IwbElement_ConflictAllForNode.md)
