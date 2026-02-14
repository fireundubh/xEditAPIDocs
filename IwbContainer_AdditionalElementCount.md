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

## See Also

- [ElementCount](IwbContainer_ElementCount.md)


