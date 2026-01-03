# ClearMessages

## Syntax

```pascal
procedure ClearMessages;
```

## Description

Clears all messages from the messages window.

This procedure removes all previously displayed messages from the xEdit messages pane, providing a clean slate for new messages.

## Example

```pascal
begin
  ClearMessages;
  AddMessage('Fresh start - previous messages cleared');
end;
```

## See Also

- [AddMessage](Global_AddMessage.md)


