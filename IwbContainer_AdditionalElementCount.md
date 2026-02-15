# AdditionalElementCount

## Syntax

```pascal
function AdditionalElementCount(AContainer: IwbContainer): integer;
```

## Description

Returns the number of "fake" elements in `AContainer`.

A fake element is one that doesn't actually exist in the record data but is shown in the UI for convenience or special handling purposes.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to count additional elements in |

## Returns

Returns the count of fake elements as an integer.

## Example

```pascal
// Example 1: Calculate total element capacity
var
  keywords: IwbContainer;
  realCount, additionalCount, totalCapacity: integer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      realCount := ElementCount(keywords);
      additionalCount := AdditionalElementCount(keywords);
      totalCapacity := realCount + additionalCount;
      AddMessage(Format('Container has %d real + %d fake = %d total slots',
        [realCount, additionalCount, totalCapacity]));
    end;
  end;
end;

// Example 2: Check if container has UI placeholder elements
var
  container: IwbContainer;
  additionalCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    additionalCount := AdditionalElementCount(container);
    if additionalCount > 0 then
      AddMessage(Format('Container shows %d UI placeholder element(s)', [additionalCount]))
    else
      AddMessage('Container has no fake elements');
  end;
end;

// Example 3: Distinguish real from fake elements during iteration
var
  container: IwbContainer;
  i, realCount, additionalCount: integer;
  element: IwbElement;
begin
  if Assigned(e) then begin
    container := e;
    realCount := ElementCount(container);
    additionalCount := AdditionalElementCount(container);

    AddMessage(Format('Processing %d real elements (skipping %d fake)',
      [realCount, additionalCount]));

    for i := 0 to realCount - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then
        AddMessage(Format('  Element %d: %s', [i, Name(element)]));
    end;
  end;
end;
```

## See Also

- [ElementCount](IwbContainer_ElementCount.md)


