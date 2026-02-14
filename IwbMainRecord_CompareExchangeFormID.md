# CompareExchangeFormID

## Syntax

```pascal
function CompareExchangeFormID(ARecord: IwbMainRecord; AOldFormID: TwbFormID; ANewFormID: TwbFormID): Boolean;
```

## Description

Attempts to change the Form ID of `ARecord` from `AOldFormID` to `ANewFormID`

Returns `True` if the attempt was successful and `False` otherwise

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to change the Form ID on |
| AOldFormID | TwbFormID | The expected current Form ID to compare against |
| ANewFormID | TwbFormID | The new Form ID to assign if the comparison matches |

## Returns

Returns `True` if the Form ID was successfully changed, `False` otherwise.

## Example

```pascal
OldFormID := GetLoadOrderFormID(e);
NewFormID := (OldFormID and $00FFFFFF) + (NewLoadOrder shl 24);

while ReferencedByCount(m) > 0 do
	CompareExchangeFormID(ReferencedByIndex(m, 0), OldFormID, NewFormID);
  
SetLoadOrderFormID(e, NewFormID);
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)


