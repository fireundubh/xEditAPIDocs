# Path

## Syntax

```pascal
function Path(AElement: IwbElement): string;
```

## Description

Returns the path component of an element.

This function returns a single piece of the full path that would be returned by `FullPath`. Useful when manually constructing paths for `ElementByPath` operations.

## Example

```pascal
var
  pathComponent: string;
begin
  pathComponent := Path(element);
end;
```

## See Also

- [ElementAssign](IwbElement_ElementAssign.md)


