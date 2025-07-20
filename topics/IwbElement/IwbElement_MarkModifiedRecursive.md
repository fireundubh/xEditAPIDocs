# MarkModifiedRecursive

## Syntax

```pascal
procedure MarkModifiedRecursive(AElement: IwbElement);
```

## Description

Marks the element and all of its descendants as modified.

This forces xEdit to serialize the marked elements. Useful when you've made changes to an element's hierarchy and need to ensure all changes are saved.

## Example

```pascal
var
    rootElement: IwbElement;
begin
    MarkModifiedRecursive(rootElement);
end;
```

## See Also

- [Check - IwbElement](IwbElement_Check.md)
