# RecordByFormID

## Syntax

```pascal
function RecordByFormID(AFile: IwbFile; AFormID: Integer; AAllowInjected: Boolean): IwbMainRecord;
```

## Description

Searches `AFile` for the main record identified by `AFormID`.

`AFormID` is a file FormID for `AFile`. The module prefix is an index into that file's master list, not a slot in the current load order. This is the value [FormID](IwbMainRecord_FormID.md) returns for a record in `AFile`, and the value [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md) returns. It is not the value [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md) returns.

How the prefix is read:

1. A prefix that names one of `AFile`'s masters is that master, counted in `AFile`'s master list.
   - On Skyrim, Fallout, and earlier games the high byte is the index in that list. Light plugins are not a separate `FE` index here. An override of a light plugin keeps the 12-bit object ID and puts that plugin's position in the master list in the high byte. In one load order, `FE003800` became `03000800`.
   - On Starfield the index is per module type. A full master uses the high byte. A light master stays in `FE` form, but the light slot is its index among `AFile`'s light masters, not its load-order light slot. A medium master uses `FD` the same way.
2. If `AFile` contains that record, that copy is returned. For an override, this is the override stored in `AFile`.
3. If `AFile` does not contain it, the same file FormID is looked up in the named master. The result is the highest override visible to `AFile`. That may be the master record, or an override in a plugin loaded before `AFile`. Check [GetFile](IwbElement_GetFile.md) if you need the copy that is actually stored in `AFile`.
4. A prefix that is not a master index means a record `AFile` itself introduced. The prefix is replaced with `AFile`'s own local module index, then the record is looked up. On games other than Starfield, that is a high byte greater than or equal to `AFile`'s master count. On Starfield the same test uses the full, light, or medium master count for that prefix.

Rule 4 is why [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md) seems to work for a native record and fails for an override.

`GetLoadOrderFormID` puts the origin plugin's current load-order slot in the prefix. The same number is a different kind of prefix from the file FormID.

- The record was created by `AFile`. Its load-order slot is `AFile`'s own position. A file is not one of its own masters, so the prefix falls into rule 4 and the lookup finds the local record. `RecordByFormID(TargetPlugin, $0B000D62, True)` can succeed in this case.
- The record is an override of another plugin. The slot is that other plugin's load-order position, not its index in `AFile`'s master list. Rule 4 then searches for a local record that is not there, or rule 1 names a different master. The call returns nil, or a different record. In the same load order, `$0B000D62` and `$FE003800` both missed, and the file FormIDs `$02000D62` and `$03000800` hit.

The two values are equal only when the origin's load-order slot happens to be the same number as its index in `AFile`. The game master (`00`) is the usual case. Do not rely on that.

Convert a load-order FormID before the lookup. The origin must be `AFile` or one of its masters. Otherwise the conversion raises.

```pascal
fileFormID := LoadOrderFormIDtoFileFormID(targetFile, GetLoadOrderFormID(rec));
hit := RecordByFormID(targetFile, fileFormID, True);
```

[RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md) is the other lookup. It throws the prefix away, keeps the object ID, and searches only records introduced by the named file. It does not find overrides.

`AAllowInjected` includes injected records when it is True.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose master list the FormID is relative to |
| AFormID | Integer | File FormID for `AFile`. Not a load-order FormID |
| AAllowInjected | Boolean | Search injected records as well when True |

## Returns

The `IwbMainRecord` for that file FormID, or nil if `AFile` and the master named by the prefix have no such record.

The record is not always stored in `AFile`. If `AFile` has no copy, the result is the highest override visible to `AFile`.

## Example

```pascal
// Example 1: Skyrim.esm is master 00 in its own file and in the load order.
// Both FormIDs are the same number. That is not true for later plugins.
var
  f: IwbFile;
  r: IwbMainRecord;
begin
  f := FileByName('Skyrim.esm');
  if Assigned(f) then
    r := RecordByFormID(f, $00013002, False);
end;

// Example 2: e may be any override of the record. GetLoadOrderFormID is the
// load-order FormID. RecordByFormID needs the file FormID for this plugin.
var
  targetFile: IwbFile;
  rec: IwbMainRecord;
  fileFormID: Cardinal;
begin
  targetFile := FileByName('MyPatch.esp');
  if Assigned(e) and Assigned(targetFile) then begin
    fileFormID := LoadOrderFormIDtoFileFormID(targetFile, GetLoadOrderFormID(e));
    rec := RecordByFormID(targetFile, fileFormID, True);
    if Assigned(rec) and Equals(GetFile(rec), targetFile) then
      AddMessage(Name(rec));
  end;
end;
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [GetFile](IwbElement_GetFile.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md)
- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)
- [RecordCount](IwbFile_RecordCount.md)
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md)
