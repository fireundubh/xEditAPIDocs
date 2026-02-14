# wbGetSiblingRecords

## Syntax

```pascal
procedure wbGetSiblingRecords(AElement: IwbElement; ASignatures: string; AIncludeOverrides: Boolean; AList: TList);
```

## Description

Finds all sibling records (records in the same group) matching the specified signatures. Sibling records are those that share the same parent group as the source element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose siblings to search |
| ASignatures | string | String containing the record signatures to match (e.g., 'NPC_CREA') |
| AIncludeOverrides | Boolean | Whether to include override records in the results |
| AList | TList | The list to receive matching sibling records as IwbMainRecord pointers |

## Returns

This function does not return a value.

## Example

```pascal
var
  record: IwbMainRecord;
  siblings: TList;
  i: Integer;
begin
  record := RecordByEditorID('DefaultPlayerVoice');
  siblings := TList.Create;
  try
    wbGetSiblingRecords(record, 'VTYP', True, siblings);

    AddMessage('Found ' + IntToStr(siblings.Count) + ' voice type records');

    for i := 0 to siblings.Count - 1 do
      AddMessage('  ' + IwbMainRecord(siblings[i]).EditorID);
  finally
    siblings.Free;
  end;
end;
```

## See Also

- [wbFindREFRsByBase](IwbResource_wbFindREFRsByBase.md)
