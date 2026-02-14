# DisplayName

## Syntax

```pascal
function DisplayName(AElement: IwbElement): string;
```

## Description

Returns a user-friendly name suitable for display in interfaces.

This function retrieves the DisplayName property with the True parameter (extended format), which provides a formatted name optimized for UI presentation. For simple elements this may be identical to Name, but for complex elements it may include additional context like values or indices. Returns an empty string for invalid elements. Commonly used in xEdit's tree view and other UI components where clarity is more important than brevity.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose display name to retrieve |

## Returns

Returns the display name of the element as a string. If no specific display name exists, returns the same value as `Name`.

## Example

```pascal
var
  element: IwbElement;
  name: string;
begin
  name := DisplayName(element);
  // Use the display name
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [BaseName](IwbElement_BaseName.md)
- [ShortName](IwbElement_ShortName.md)
- [PathName](IwbElement_PathName.md)


