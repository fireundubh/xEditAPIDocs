# PathName

## Syntax

```pascal
function PathName(AElement: IwbElement): string;
```

## Description

Returns the path and name of the element combined.

This function combines the element's path and name into a single string, providing a more complete identifier for the element than either Path or Name alone.

## Example

```pascal
var
  element: IwbElement;
  pathAndName: string;
begin
  pathAndName := PathName(element);
  // Might return something like "WRLD\Tamriel"
end;
```

## See Also

- [Path - IwbElement](IwbElement_Path.md)
- [Name - IwbElement](IwbElement_Name.md)
- [FullPath - IwbElement](IwbElement_FullPath.md)
