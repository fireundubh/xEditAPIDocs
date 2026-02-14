# PathName

## Syntax

```pascal
function PathName(AElement: IwbElement): string;
```

## Description

Returns the element's path name, combining structural and display information.

This function retrieves the PathName property, which provides a hybrid identifier combining path and name information. The exact format depends on the element type but generally includes the element's position and identifier within its parent. More descriptive than Path alone but not as comprehensive as FullPath. Returns an empty string for invalid elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the combined path and name for |

## Returns

Returns the combined path and name as a string.

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

- [Path](IwbElement_Path.md)
- [FullPath](IwbElement_FullPath.md)
- [IndexedPath](IwbElement_IndexedPath.md)
- [Name](IwbElement_Name.md)
- [DisplayName](IwbElement_DisplayName.md)


