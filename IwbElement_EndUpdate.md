# EndUpdate

## Syntax

```pascal
procedure EndUpdate(AElement: IwbElement);
```

## Description

Ends an update batch for the element and processes any deferred notifications.

This function calls the element's EndUpdate method, which decrements the internal update counter. When the counter reaches zero, all deferred change notifications are processed and the element is marked as modified. Must be called once for each BeginUpdate. Always use in a try-finally block to guarantee execution even if errors occur during updates.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to end bulk updates on |

## Example

```pascal
BeginUpdate(e);
try
  // many changes to e
finally
  EndUpdate(e);
end;
```

## See Also

- [BeginUpdate](IwbElement_BeginUpdate.md)
