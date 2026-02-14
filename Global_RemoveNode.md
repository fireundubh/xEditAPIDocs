# RemoveNode

## Syntax

```pascal
function RemoveNode(AElement: IwbElement): Boolean;
```

## Description

Removes an element and its corresponding node from the navigation tree view. This function safely removes the element from both the user interface and the data structure, clearing history references if it's a main record.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to remove from the tree view |

## Returns

Returns True if the node was successfully found and removed, False otherwise.

## Example

```pascal
var
  record: IwbMainRecord;
begin
  record := RecordByEditorID('MyCustomRecord');

  if Assigned(record) then begin
    if RemoveNode(record) then
      AddMessage('Record removed from view');
  end;
end;
```

## See Also

- [Remove](IwbElement_Remove.md)
