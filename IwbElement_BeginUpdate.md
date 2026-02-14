# BeginUpdate

## Syntax

```pascal
procedure BeginUpdate(AElement: IwbElement);
```

## Description

Begins an update batch for the element to defer notifications and improve performance.

This function calls the element's BeginUpdate method, which increments an internal update counter. While in update mode, the element defers change notifications and UI updates. Multiple BeginUpdate calls can be nested, and each must be matched with a corresponding EndUpdate. Always use in a try-finally block to ensure EndUpdate is called. Returns the new update counter value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to begin bulk updates on |

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

- [EndUpdate](IwbElement_EndUpdate.md)
