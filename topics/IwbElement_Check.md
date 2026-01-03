# Check

## Syntax

```pascal
function Check(AElement: IwbElement): string;
```

## Description

Performs an error check on the specified element.

Returns the error message produced when the "Check for Errors" functionality is run on the element. If no error is found, returns an empty string.

## Example

```pascal
var
  element: IwbElement;
  errorMessage: string;
begin
  errorMessage := Check(element);
  if errorMessage <> '' then
    // Handle the error condition
end;
```

## See Also

- [Assigned - IwbElement](IwbElement_Assigned.md)


