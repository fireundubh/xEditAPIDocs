# BeginUpdate

## Syntax

```pascal
procedure BeginUpdate(AElement: IwbElement);
```

## Description

Starts a bulk update for `AElement`. This can improve performance when making many changes to an element.

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
