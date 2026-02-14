# wbFindREFRsByBase

## Syntax

```pascal
procedure wbFindREFRsByBase(aMainRecord: IwbMainRecord; aBaseSignatures: string; aOptions: Integer; aList: TList);
```

## Description

Finds all reference (REFR) records in child groups of a worldspace or cell that reference base records with specified signatures. The function can filter out deleted, disabled, or enable state parent references based on options.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aMainRecord | IwbMainRecord | The worldspace or cell record to search within |
| aBaseSignatures | string | String containing the base record signatures to search for (e.g., 'TREESTAT') |
| aOptions | Integer | Bitmask options: 1=skip deleted, 2=skip disabled, 4=skip enable state parent |
| aList | TList | The list to receive matching reference records as IwbMainRecord pointers |

## Returns

This function does not return a value.

## Example

```pascal
var
  worldspace: IwbMainRecord;
  treeRefs: TList;
  i: Integer;
begin
  worldspace := RecordByEditorID('Tamriel');
  treeRefs := TList.Create;
  try
    // Find all non-deleted, non-disabled tree references
    wbFindREFRsByBase(worldspace, 'TREE', 3, treeRefs);

    AddMessage('Found ' + IntToStr(treeRefs.Count) + ' tree references');

    for i := 0 to treeRefs.Count - 1 do
      AddMessage('  ' + IwbMainRecord(treeRefs[i]).Name);
  finally
    treeRefs.Free;
  end;
end;
```

## See Also

- [wbGetSiblingRecords](IwbResource_wbGetSiblingRecords.md)
