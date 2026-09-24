# RecordFromFileByFormID

## Syntax

```pascal
function RecordFromFileByFormID(AFile: IwbFile|string; AFormID: integer|string): IwbMainRecord;
```

## Description

Returns the main record in one file whose local object ID matches `AFormID`.

`AFile` may be an `IwbFile` or a loaded filename. `AFormID` may be an integer or a hex string. Leading zeroes in the hex string are optional.

The module prefix on `AFormID` does not have to match the current load order. The function throws that prefix away, keeps the local object ID, and looks the record up under the named file's own module index. That is why a FormID copied from another session, a log, or an older load order still resolves, including an ESL FormID, as long as you name the file that owns the record.

What happens to `AFormID`:

1. The prefix may be stale. It is not used as a load-order index.
2. The local object ID is what remains. How many bits are kept depends on the file you named:
   - Normal ESM or ESP: the low 24 bits (the last six hex digits).
   - Medium master, on games that have them: the low 16 bits (the last four hex digits).
   - Light plugin (an `.esl`, or a plugin with the light / small-master flag): the low 12 bits (the last three hex digits).
3. A value that already looks like a light or medium FormID is read at that width first. On games that support light plugins, a high byte of `FE` means only the last three hex digits are the object ID. On games that support medium masters, a high byte of `FD` means only the last four. The file's own type can only shorten that further. It cannot put those digits back. `FE003001` is object `001`, not `003001`, even when the file you pass is a normal plugin.
4. The named file's current load-order module index replaces the prefix, and the record is looked up in that file. Injected records are included.

The usual case is a record introduced by that file. An override of another file's record keeps the other file's FormID, so passing the master FormID and a patch filename does not find the override. Use [RecordByFormID](IwbFile_RecordByFormID.md) with that patch's file FormID. [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md) converts a load-order FormID into that value. Passing the load-order FormID straight to `RecordByFormID` does not find the override.

Pass the returned record to [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md) when you need its FormID in this session's load order.

| Supplied FormID | File you named | Object ID used |
|-----------------|----------------|----------------|
| `0000000F` | normal plugin | `00000F` |
| `05001234` | normal plugin | `001234` |
| `05001234` | medium master | `1234` |
| `05001234` | light plugin | `234` |
| `FE003001` | any file, when light plugins are supported | `001` |
| `FD003001` | normal or medium, when medium masters are supported | `3001` |
| `FD003001` | light plugin | `001` |

`1234` and `001234` are the same object ID. The medium mask only drops digits when the value is wider than 16 bits. The light mask is what reduces `05001234` to `234`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile or string | The file to search, as an `IwbFile` or as the filename of a loaded file |
| AFormID | integer or string | FormID to resolve. The module prefix may be stale; only the local object ID is used, masked to the file's type |

## Returns

The file's `IwbMainRecord` for that object ID, or nil if the file is loaded but has no such record.

A filename that is not loaded raises an error. It does not return nil.

## Example

```pascal
// Example 1: File and FormID may each be an interface/integer or a string
var
  eFile: IwbFile;
  rec: IwbMainRecord;
begin
  eFile := FileByName('Skyrim.esm');
  rec := RecordFromFileByFormID(eFile, $0000000F);
  rec := RecordFromFileByFormID(eFile, '0000000F');
  rec := RecordFromFileByFormID('Skyrim.esm', '0000000F');
end;

// Example 2: Prefix 05 is from another load order. Only 001234 is used.
// GetLoadOrderFormID reports MyMod.esp's slot in this session.
var
  rec: IwbMainRecord;
  loadOrderFormID: Cardinal;
begin
  rec := RecordFromFileByFormID('MyMod.esp', '05001234');
  if Assigned(rec) then begin
    loadOrderFormID := GetLoadOrderFormID(rec);
    AddMessage('Load order FormID: ' + IntToHex(loadOrderFormID, 8));
  end;
end;

// Example 3: FE003 is a light slot from another load order.
// The object ID is 001. GetLoadOrderFormID prints the file's current light slot.
var
  rec: IwbMainRecord;
begin
  rec := RecordFromFileByFormID('MyMod.esl', 'FE003001');
  if Assigned(rec) then
    AddMessage('Load order FormID: ' + IntToHex(GetLoadOrderFormID(rec), 8));
end;
```

## See Also

- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)
