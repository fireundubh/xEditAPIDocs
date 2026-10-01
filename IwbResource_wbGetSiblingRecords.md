# wbGetSiblingRecords

## Syntax

```pascal
procedure wbGetSiblingRecords(AElement: IwbElement; ASignatures: string; AOverrides: Boolean; AList: TList);
```

## Description

Fills `AList` with main records of the given signatures. Despite the name, a main record is not searched for records that share its parent. The search looks in that record's child group.

`AOverrides` also searches the child groups of later overrides of that same record. Copies that share a load-order FormID are reduced to the later one. When `AElement` is a group or a file rather than a main record, the flag is ignored and the search walks that container only. A main record that does not itself match is not entered, so a file or a worldspace does not yield references stored inside cells. Pass the cell for those.

If `AElement` is not an element, or `AList` is nil, the call returns without adding anything.

Separate signatures with commas or with spaces. Each token is trimmed, and the first four characters are the signature. `'REFR,ACHR'` matches both. `'NPC_CREA'` has no separator, so only `NPC_` is used.

Read each hit with `ObjectToElement`. Do not write `AList[i].EditorID`. Free the list when you are done. You create it; this call does not.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | Main record whose child group is searched, or a group or file to walk directly |
| ASignatures | string | Signatures separated by commas or spaces, such as `'REFR,ACHR'` |
| AOverrides | Boolean | For a main record, also search later overrides and keep the later copy of each FormID |
| AList | TList | Caller-owned list that receives the records |

## Returns

This procedure does not return a value.

## Example

```pascal
var
  plugin: IwbFile;
  cell, rec: IwbMainRecord;
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
    wbGetSiblingRecords(cell, 'REFR,ACHR', True, refs);
    for i := 0 to Pred(refs.Count) do begin
      rec := ObjectToElement(refs[i]);
      if Assigned(rec) then
        AddMessage(EditorID(rec));
    end;
  finally
    refs.Free;
  end;
end;
```

## See Also

- [wbFindREFRsByBase](IwbResource_wbFindREFRsByBase.md)
- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [ObjectToElement](Global_ObjectToElement.md)
