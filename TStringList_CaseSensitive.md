# TStringList.CaseSensitive

## Syntax

```pascal
property CaseSensitive: Boolean;
```

## Description

Determines whether string comparisons are case-sensitive.

## Parameters

This property has no parameters.

## Returns

Boolean. Reading the property returns whether string comparisons on this list are case-sensitive.

## Example

```pascal
var
  list: TStringList;
begin
  list := TStringList.Create;
  try
    list.CaseSensitive := True;
    if list.CaseSensitive then
      AddMessage('List is case-sensitive');
  finally
    list.Free;
  end;
end;
```
