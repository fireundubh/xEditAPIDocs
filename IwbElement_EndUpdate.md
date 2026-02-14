# EndUpdate

## Syntax

```pascal
procedure EndUpdate(AElement: IwbElement);
```

## Description

Ends a bulk update for `AElement`.

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
