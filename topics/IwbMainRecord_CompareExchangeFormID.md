# CompareExchangeFormID

## Syntax

```pascal
function CompareExchangeFormID(ARecord: IwbMainRecord; AOldFormID: TwbFormID; ANewFormID: TwbFormID): Boolean;
```

## Description

Attempts to change the Form ID of `ARecord` from `AOldFormID` to `ANewFormID`

Returns `True` if the attempt was successful and `False` otherwise

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


