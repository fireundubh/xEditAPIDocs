# ConflictAllForNode

## Syntax

```pascal
function ConflictAllForNode(AElement: IwbElement): TConflictAll;
```

## Description

Gets the overall conflict status for a node and its children.

Returns a `TConflictAll` enumeration value representing the conflict state for the specified element and all its child elements.

## Example

```pascal
var
  conflict: TConflictAll;
begin
  conflict := ConflictAllForNode(someElement);
end;
```

## See Also

- [ConflictThisForNode](IwbElement_ConflictThisForNode.md)


