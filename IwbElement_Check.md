# Check

## Syntax

```pascal
function Check(AElement: IwbElement): string;
```

## Description

Validates the element and returns any error message found.

This function calls the element's Check method, which performs validation based on the element's definition rules (required fields, value constraints, reference validity, etc.). This is the same validation used by xEdit's "Check for Errors" feature. Returns an empty string if the element is valid or if validation is not applicable. Returns a descriptive error message if validation fails. Use this to verify record integrity before saving.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check for errors |

## Returns

Returns the error message as a string, or an empty string if no error is found.

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


