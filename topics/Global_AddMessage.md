# AddMessage

## Syntax

```pascal
procedure AddMessage(AText: string);
```

## Description

Prints `AText` to the Messages pane

Multiple strings can be concatenated with the `+` operator.

To pass variables in `AText`, convert non-string variables to strings with functions such as `IntToStr` for integers.

To pass special characters in `AText`, concatenate the string with character literals such as `#9` for `\t` (TAB).

## Example

```pascal
AddMessage('Listing loaded files...');

for i := 0 to Pred(FileCount) do
begin
    f := FileByIndex(i);
    
    AddMessage(GetFileName(f) + ' is loaded at index: ' + IntToStr(i));
    
    r := RecordByIndex(f, 0);
  
    if Assigned(r) then
        AddMessage(#9 + 'Its first record is: ' + Name(r))
    else
        AddMessage(#9 + 'No first record exists.');
end;
```

## See Also

- [ClearMessages](Global_ClearMessages.md)


