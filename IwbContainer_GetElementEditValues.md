# GetElementEditValues

## Syntax

```pascal
function GetElementEditValues(AContainer: IwbContainer; APath: string): string;
```

## Description

Returns the edit value of an element in the container by path as a string. This is the value as it would appear in the editor.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve the value from |
| APath | string | The element path to the value |

## Returns

Returns the edit value as a string.

## Example

```pascal
var
  value: string;
begin
  value := GetElementEditValues(container, 'FULL'); // Get full name
end;
```

## See Also

- [SetElementEditValues](IwbContainer_SetElementEditValues.md)
- [GetElementNativeValues](IwbContainer_GetElementNativeValues.md)
- [GetElementValues](IwbContainer_GetElementValues.md)
- [GetEditValue](IwbElement_GetEditValue.md)


