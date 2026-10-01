# wbFindREFRsByBase

## Syntax

```pascal
procedure wbFindREFRsByBase(AMainRecord: IwbMainRecord; ABaseSignatures: string; AOptions: Integer; AList: TList);
```

## Description

Fills `AList` with placed references whose base record has one of the given signatures. The search looks in the child group of `AMainRecord` for `REFR` records, and also in the child groups of later overrides of that same record. When the same FormID appears more than once, the later copy is kept.

Pass a cell. A worldspace's child group holds cells and cell blocks, and this search does not enter those cells, so a worldspace does not yield its references. If `AMainRecord` is not a main record, or `AList` is nil, the call returns without adding anything.

`ABaseSignatures` is matched with a substring search against the base record's signature. Signatures are four uppercase characters, so `'STAT'` matches and `'stat'` does not. `'STATCONT'` matches both. A separator is allowed.

`AOptions` is a bit mask. Bit 1 skips deleted references, bit 2 skips references that are initially disabled, and bit 4 skips references that have an `XESP` element. Zero keeps all three.

Read each hit with `ObjectToElement`. Do not write `AList[i].Name`. Free the list when you are done. You create it; this call does not.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AMainRecord | IwbMainRecord | Cell whose child group is searched. Not a worldspace |
| ABaseSignatures | string | Uppercase signatures to find on the base record, such as `'STAT'` or `'STATCONT'` |
| AOptions | Integer | Bit 1 skips deleted, bit 2 skips initially disabled, bit 4 skips `XESP` |
| AList | TList | Caller-owned list that receives the references |

## Returns

This procedure does not return a value.

## Example

```pascal
var
  plugin: IwbFile;
  cell, refr: IwbMainRecord;
  refs: TList;
  i: Integer;
begin
  plugin := FileByName('Skyrim.esm');
  if not Assigned(plugin) then
    Exit;

  cell := RecordByEditorID(plugin, 'WhiterunDragonsreach');
  if not Assigned(cell) then
    Exit;

  refs := TList.Create;
  try
    wbFindREFRsByBase(cell, 'FURN', 1, refs);
    for i := 0 to Pred(refs.Count) do begin
      refr := ObjectToElement(refs[i]);
      if Assigned(refr) then
        AddMessage(Name(refr));
    end;
  finally
    refs.Free;
  end;
end;
```

## See Also

- [wbGetSiblingRecords](IwbResource_wbGetSiblingRecords.md)
- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [ObjectToElement](Global_ObjectToElement.md)
