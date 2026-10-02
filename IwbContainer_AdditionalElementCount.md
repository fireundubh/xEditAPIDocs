# AdditionalElementCount

## Syntax

```pascal
function AdditionalElementCount(AContainer: IwbContainer): integer;
```

## Description

Returns how many leading children are not ordinary stored members.

For most containers the result is 0. A main record returns 1 for the record header, or 2 when a Contained In element is also present. Those children are already included in [ElementCount](IwbContainer_ElementCount.md); ordinary members start at index `AdditionalElementCount`. Returns 0 if the argument is not a container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to count additional elements in |

## Returns

An integer. 0 for an ordinary container or when the argument is not a container. 1 or 2 for a main record. These elements are already part of `ElementCount`.

## Example

```pascal
// Example 1: Skip the record header when walking a main record
var
  i, firstReal: integer;
  child: IwbElement;
begin
  if Assigned(e) then begin
    firstReal := AdditionalElementCount(e);
    AddMessage('Leading non-members: ' + IntToStr(firstReal));

    for i := firstReal to Pred(ElementCount(e)) do begin
      child := ElementByIndex(e, i);
      if Assigned(child) then
        AddMessage(Format('  [%d] %s', [i, Name(child)]));
    end;
  end;
end;

// Example 2: An ordinary array has no leading non-members
var
  keywords: IwbContainer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then
      AddMessage('KWDA additional count: ' + IntToStr(AdditionalElementCount(keywords)));
  end;
end;
```

## See Also

- [ElementCount](IwbContainer_ElementCount.md)


