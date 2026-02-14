# ContainingMainRecord

## Syntax

```pascal
function ContainingMainRecord(AElement: IwbElement): IwbMainRecord;
```

## Description

Retrieves the main record that contains the specified element.

Returns the parent main record that contains the given element. This is useful when working with sub-records or other nested elements and you need to access their containing record.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the containing main record for |

## Returns

Returns the containing main record as an IwbMainRecord interface.

## Example

```pascal
var
  element: IwbElement;
  mainRecord: IwbMainRecord;
begin
  mainRecord := ContainingMainRecord(element);
  if Assigned(mainRecord) then
    // Work with the main record
end;
```

## See Also

- [GetContainer](IwbElement_GetContainer.md)


