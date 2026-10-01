# JumpTo

## Syntax

```pascal
procedure JumpTo(ARecord: IwbMainRecord; ABackward: Boolean);
```

## Description

Selects a main record in the xEdit user interface.

`ARecord` must be a main record. Any other element raises an invalid-argument error. The call does not walk from a subrecord up to its containing record.

`ABackward` chooses which history list receives the view that is current before the jump. False puts that view on the back list. True puts it on the forward list. The flag does not search through records.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | Main record to select |
| ABackward | Boolean | True stores the current view on the forward history. False stores it on the back history |

## Returns

Nothing.

## Example

```pascal
begin
  if Assigned(e) then
    JumpTo(e, False);
end;
```

## See Also

- [Signature](IwbMainRecord_Signature.md)
