# ContainingMainRecord

## Syntax

```pascal
function ContainingMainRecord(AElement: IwbElement): IwbMainRecord;
```

## Description

Retrieves the main record that contains the specified element.

Returns the parent main record that contains the given element. This is useful when working with sub-records or other nested elements and you need to access their containing record.

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

- [GetContainer - IwbElement](IwbElement_GetContainer.md)
