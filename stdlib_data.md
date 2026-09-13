# Data Structures Reference

Data structure classes for managing lists, strings, streams, collections, and components in xEdit scripts.

**Units:** Classes, System

[← Back to Standard Library Overview](stdlib_home.md)

## Table of Contents

- [TList - Object List](#tlist---object-list)
- [TStrings and TStringList](#tstrings-and-tstringlist)
- [Stream Classes](#stream-classes)
- [TCollection and TCollectionItem](#tcollection-and-tcollectionitem)
- [TPersistent and TComponent](#tpersistent-and-tcomponent)
- [xEdit Data Management Examples](#xedit-data-management-examples)

## TList - Object List

TList manages a dynamic array of pointers (can store objects, records, or any pointer type).

**Constructor:**
```pascal
list := TList.Create;
```

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `Count` | Integer | Number of items |
| `Capacity` | Integer | Allocated capacity |
| `Items[Index]` | Pointer | Item at index (0-based) |

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `Add` | `Add(Item: Pointer): Integer` | Add item, returns index |
| `Insert` | `Insert(Index: Integer, Item: Pointer)` | Insert at index |
| `Delete` | `Delete(Index: Integer)` | Remove item at index |
| `Remove` | `Remove(Item: Pointer): Integer` | Remove first occurrence, returns index |
| `Clear` | `Clear()` | Remove all items |
| `IndexOf` | `IndexOf(Item: Pointer): Integer` | Find item index (-1 if not found) |
| `First` | `First(): Pointer` | First item (nil if empty) |
| `Last` | `Last(): Pointer` | Last item (nil if empty) |
| `Exchange` | `Exchange(Index1, Index2: Integer)` | Swap two items |
| `Move` | `Move(CurIndex, NewIndex: Integer)` | Move item to new position |
| `Sort` | `Sort(Compare: TListSortCompare)` | Registered, but the compare argument is a native callback. Do not pass a script function. |

### TList Example

```pascal
// Store and manage record references
var
  list: TList;
  i: Integer;
  rec: IwbMainRecord;
begin
  list := TList.Create;
  try
    // Add records to list
    for i := 0 to RecordCount(FileByIndex(0)) - 1 do begin
      rec := RecordByIndex(FileByIndex(0), i);
      if Signature(rec) = 'WEAP' then
        list.Add(Pointer(i));  // Store index
    end;

    AddMessage(Format('Found %d weapon records', [list.Count]));

    // Process list
    for i := 0 to list.Count - 1 do begin
      rec := RecordByIndex(FileByIndex(0), Integer(list[i]));
      AddMessage(EditorID(rec));
    end;

    // Clear list
    list.Clear;
  finally
    list.Free;
  end;
end;
```

**Note:** TList stores pointers, which has limited use in JvInterpreter since **custom pointer type definitions** (like `PMyRecord = ^TMyRecord`) and memory allocation functions `New()` and `Dispose()` are not supported. However, built-in pointer types like `PChar` and `Pointer` work fine. For storing collections of objects, TStringList with the Objects property is often more convenient.

## TStrings and TStringList

TStrings is the abstract base class for string lists. TStringList is the concrete implementation.

**Constructor:**
```pascal
list := TStringList.Create;
```

### TStrings Properties

| Property | Type | Description |
|----------|------|-------------|
| `Count` | Integer | Number of strings |
| `Strings[Index]` | string | String at index (default property) |
| `Objects[Index]` | TObject | Associated object |
| `Names[Index]` | string | Name part of Name=Value pair |
| `Values[Name]` | string | Value for Name=Value pair |
| `Text` | string | All strings as single text (CRLF separated) |
| `CommaText` | string | Comma-separated list |
| `Delimiter` | Char | Delimiter character |
| `QuoteChar` | Char | Quote character |

### TStrings Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `Add` | `Add(S: string): Integer` | Add string, returns index |
| `AddObject` | `AddObject(S: string, AObject: TObject): Integer` | Add string with object |
| `Insert` | `Insert(Index: Integer, S: string)` | Insert at index |
| `Delete` | `Delete(Index: Integer)` | Remove at index |
| `Clear` | `Clear()` | Remove all strings |
| `IndexOf` | `IndexOf(S: string): Integer` | Find string (-1 if not found) |
| `IndexOfName` | `IndexOfName(Name: string): Integer` | Find Name in Name=Value pairs |
| `IndexOfObject` | `IndexOfObject(AObject: TObject): Integer` | Find object |
| `Append` | `Append(S: string)` | Append string |
| `AddStrings` | `AddStrings(Strings: TStrings)` | Add all strings from another list |
| `Assign` | `Assign(Source: TPersistent)` | Copy from another string list |
| `Exchange` | `Exchange(Index1, Index2: Integer)` | Swap two strings |
| `Move` | `Move(CurIndex, NewIndex: Integer)` | Move string |
| `BeginUpdate` | `BeginUpdate()` | Begin batch update |
| `EndUpdate` | `EndUpdate()` | End batch update |

### TStringList-Specific Properties

| Property | Type | Description |
|----------|------|-------------|
| `Duplicates` | TDuplicates | Duplicate handling (dupIgnore, dupAccept, dupError) |
| `Sorted` | Boolean | Auto-sort (must be False to add) |
| `CaseSensitive` | Boolean | Case-sensitive operations |

### TStringList-Specific Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `Sort` | `Sort()` | Sort strings |
| `Find` | `Find(S: string, var Index: Integer): Boolean` | Binary search (requires sorted) |

### String List Set Operations

TStringList set operations are **in-place procedures** on `Self`. They sort `Self`, set `Duplicates := dupIgnore`, then replace `Self` with the result. They do not return a new list.

| Method | Signature | Description |
|--------|-----------|-------------|
| `Intersection` | `procedure Intersection(List: TStringList)` | `Self := Self ∩ List` |
| `Union` | `procedure Union(List: TStringList)` | `Self := Self ∪ List` |
| `Difference` | `procedure Difference(List: TStringList)` | `Self := Self − List` |
| `SymmetricDifference` | `procedure SymmetricDifference(List: TStringList)` | `Self := (Self ∪ List) − (Self ∩ List)` |

Call `list1.Union(list2)`, not `combined := list1.Union(list2)`. See [Union](TStringList_Union.md).

### Basic TStringList Examples

#### Simple String List
```pascal
// Create and use string list
var
  list: TStringList;
  i: Integer;
begin
  list := TStringList.Create;
  try
    // Add strings
    list.Add('Apple');
    list.Add('Banana');
    list.Add('Cherry');

    // Access strings
    for i := 0 to list.Count - 1 do
      AddMessage(list[i]);

    // Find string
    if list.IndexOf('Banana') >= 0 then
      AddMessage('Found Banana');

    // Sort
    list.Sort;

    // Save to file
    list.SaveToFile(wbDataPath + 'fruits.txt');
  finally
    list.Free;
  end;
end;
```

#### Name-Value Pairs
```pascal
// Store configuration as Name=Value pairs
var
  config: TStringList;
begin
  config := TStringList.Create;
  try
    // Add name-value pairs
    config.Values['Author'] := 'My Name';
    config.Values['Version'] := '1.0';
    config.Values['Date'] := DateToStr(Now());

    // Alternative syntax
    config.Add('Description=My Plugin');

    // Read values
    AddMessage('Author: ' + config.Values['Author']);
    AddMessage('Version: ' + config.Values['Version']);

    // Save as INI-style file
    config.SaveToFile(wbDataPath + 'config.txt');
  finally
    config.Free;
  end;
end;
```

#### Associated Objects
```pascal
// Store objects with strings
var
  list: TStringList;
  i: Integer;
  rec: IwbMainRecord;
begin
  list := TStringList.Create;
  try
    // Add EditorIDs with record indices as objects
    for i := 0 to RecordCount(FileByIndex(0)) - 1 do begin
      rec := RecordByIndex(FileByIndex(0), i);
      list.AddObject(EditorID(rec), TObject(i));
    end;

    // Find and retrieve
    i := list.IndexOf('PlayerRef');
    if i >= 0 then begin
      rec := RecordByIndex(FileByIndex(0), Integer(list.Objects[i]));
      AddMessage('Found: ' + Name(rec));
    end;
  finally
    list.Free;
  end;
end;
```

### Set Operations Examples

#### Intersection (Common Items)
```pascal
// Find EditorIDs that appear in both files
var
  list1, list2: TStringList;
  i: Integer;
  rec: IwbMainRecord;
begin
  list1 := TStringList.Create;
  list2 := TStringList.Create;
  try
    for i := 0 to RecordCount(FileByIndex(0)) - 1 do begin
      rec := RecordByIndex(FileByIndex(0), i);
      list1.Add(EditorID(rec));
    end;

    for i := 0 to RecordCount(FileByIndex(1)) - 1 do begin
      rec := RecordByIndex(FileByIndex(1), i);
      list2.Add(EditorID(rec));
    end;

    list1.Intersection(list2);
    AddMessage(Format('Common EditorIDs: %d', [list1.Count]));
    for i := 0 to list1.Count - 1 do
      AddMessage('  ' + list1[i]);
  finally
    list1.Free;
    list2.Free;
  end;
end;
```

#### Union (All Unique Items)
```pascal
// Combine two lists without duplicates
var
  list1, list2: TStringList;
begin
  list1 := TStringList.Create;
  list2 := TStringList.Create;
  try
    list1.Add('Apple');
    list1.Add('Banana');

    list2.Add('Banana');
    list2.Add('Cherry');

    list1.Union(list2);
    // list1 is now Apple, Banana, Cherry
    AddMessage(Format('Combined: %d items', [list1.Count]));
  finally
    list1.Free;
    list2.Free;
  end;
end;
```

#### Difference (Items Only in First)
```pascal
// Find EditorIDs in first file but not in second
var
  list1, list2: TStringList;
begin
  // ... populate list1 and list2 ...

  list1.Difference(list2);
  AddMessage(Format('Unique to first file: %d', [list1.Count]));
end;
```

#### Symmetric Difference (Items in Either but Not Both)
```pascal
// Find EditorIDs unique to each file
var
  list1, list2: TStringList;
begin
  // ... populate list1 and list2 ...

  list1.SymmetricDifference(list2);
  AddMessage(Format('Unique items: %d', [list1.Count]));
end;
```

### File Operations

See [File Operations Reference](stdlib_files.md#tstringlist-file-operations) for `LoadFromFile`, `SaveToFile`, etc.

## Stream Classes

Stream classes provide flexible data I/O. All inherit from TStream.

### TStream Base Class

Abstract base class for all streams.

| Property | Type | Description |
|----------|------|-------------|
| `Position` | Int64 | Current position |
| `Size` | Int64 | Stream size |

| Method | Signature | Description |
|--------|-----------|-------------|
| `Read` | `Read(var Buffer; Count: Longint): Longint` | Read bytes |
| `Write` | `Write(const Buffer; Count: Longint): Longint` | Write bytes |
| `Seek` | `Seek(Offset: Integer, Origin: Integer): Integer` | Move position. Origin: 0=start, 1=current, 2=end |
| `CopyFrom` | `CopyFrom(Source: TStream, Count: Int64): Int64` | Copy from stream |
| `ReadBuffer` | `ReadBuffer(var Buffer; Count: Longint)` | Read exact bytes (raises exception on error) |
| `WriteBuffer` | `WriteBuffer(const Buffer; Count: Longint)` | Write exact bytes |

**Seek origin** is an integer (these names are not registered): `0` from start, `1` from current, `2` from end.

### TFileStream

Read and write files.

**Constructor:**
```pascal
fs := TFileStream.Create(FileName: string, Mode: Word);
```

**Mode constants:**
```pascal
fmCreate        = $FF00;  // Create new file
fmOpenRead      = $0000;  // Read only
fmOpenWrite     = $0001;  // Write only
fmOpenReadWrite = $0002;  // Read and write

// Share modes (can be combined with OR)
fmShareExclusive = $0010;  // Exclusive access
fmShareDenyWrite = $0020;  // Allow read, deny write
fmShareDenyRead  = $0030;  // Allow write, deny read
fmShareDenyNone  = $0040;  // Allow all
```

### TMemoryStream

Work with data in memory.

**Constructor:**
```pascal
ms := TMemoryStream.Create;
```

| Method | Signature | Description |
|--------|-----------|-------------|
| `LoadFromFile` | `LoadFromFile(FileName: string)` | Load file into memory |
| `SaveToFile` | `SaveToFile(FileName: string)` | Save to file |
| `LoadFromStream` | `LoadFromStream(Stream: TStream)` | Load from stream |

### TStringStream

Work with strings as streams.

**Constructor:**
```pascal
ss := TStringStream.Create(const AString: string);
```

| Property | Type | Description |
|----------|------|-------------|
| `DataString` | string | String content |

### Stream Examples

See [File Operations Reference](stdlib_files.md#stream-classes) for detailed stream examples.

## TCollection and TCollectionItem

TCollection manages a collection of TCollectionItem objects.

### TCollection

**Constructor:**
```pascal
coll := TCollection.Create(ItemClass: TCollectionItemClass);
```

| Property | Type | Description |
|----------|------|-------------|
| `Count` | Integer | Number of items |
| `Items[Index]` | TCollectionItem | Item at index |

| Method | Signature | Description |
|--------|-----------|-------------|
| `Add` | `Add(): TCollectionItem` | Add new item |
| `Clear` | `Clear()` | Remove all items |
| `Delete` | `Delete(Index: Integer)` | Delete item |
| `Insert` | `Insert(Index: Integer): TCollectionItem` | Insert new item |
| `BeginUpdate` | `BeginUpdate()` | Begin batch update |
| `EndUpdate` | `EndUpdate()` | End batch update |

### TCollectionItem

Base class for collection items.

| Property | Type | Description |
|----------|------|-------------|
| `Collection` | TCollection | Owner collection |
| `Index` | Integer | Item index |

## TPersistent and TComponent

Base classes for Delphi objects.

### TPersistent

Base class for objects that can be assigned and persisted.

| Method | Signature | Description |
|--------|-----------|-------------|
| `Assign` | `Assign(Source: TPersistent)` | Copy from another object |

### TComponent

Base class for components.

| Property | Type | Description |
|----------|------|-------------|
| `Owner` | TComponent | Component owner |
| `Name` | string | Component name |
| `Tag` | Integer | User-defined integer |
| `ComponentCount` | Integer | Number of owned components |
| `Components[Index]` | TComponent | Owned component |

| Method | Signature | Description |
|--------|-----------|-------------|
| `FindComponent` | `FindComponent(Name: string): TComponent` | Find by name |
| `InsertComponent` | `InsertComponent(AComponent: TComponent)` | Add owned component |
| `RemoveComponent` | `RemoveComponent(AComponent: TComponent)` | Remove owned component |
| `FreeNotification` | `FreeNotification(AComponent: TComponent)` | Request free notification |

## xEdit Data Management Examples

### Example 1: Record Cache

```pascal
// Cache EditorID -> record index
var
  cache: TStringList;
  i, idx: Integer;
  rec: IwbMainRecord;
  aFile: IwbFile;
begin
  aFile := FileByIndex(0);
  cache := TStringList.Create;
  try
    cache.Sorted := True;
    cache.Duplicates := dupIgnore;

    for i := 0 to RecordCount(aFile) - 1 do begin
      rec := RecordByIndex(aFile, i);
      cache.AddObject(EditorID(rec), TObject(i));
    end;

    if cache.Find('PlayerRef', idx) then begin
      rec := RecordByIndex(aFile, Integer(cache.Objects[idx]));
      AddMessage('Found: ' + Name(rec));
    end;
  finally
    cache.Free;
  end;
end;
```

### Example 2: Export Record Hierarchy

```pascal
// Export hierarchical record data
var
  output: TStringList;
  indent: Integer;

procedure ExportElement(el: IwbElement; level: Integer);
var
  i: Integer;
  spaces: string;
begin
  spaces := StringOfChar(' ', level * 2);
  output.Add(Format('%s%s: %s', [spaces, Name(el), GetEditValue(el)]));

  for i := 0 to ElementCount(el) - 1 do
    ExportElement(ElementByIndex(el, i), level + 1);
end;

begin
  output := TStringList.Create;
  try
    indent := 0;

    // Export record hierarchy
    ExportElement(e, 0);

    // Save to file
    output.SaveToFile(wbDataPath + 'record_export.txt');
    AddMessage(Format('Exported %d lines', [output.Count]));
  finally
    output.Free;
  end;
end;
```

### Example 3: Binary Data Processing

```pascal
// Read and process binary record data
var
  ms: TMemoryStream;
  fs: TFileStream;
  signature: array[0..3] of Char;
  formID: Cardinal;
  flags: Word;
begin
  ms := TMemoryStream.Create;
  try
    // Load plugin file
    fs := TFileStream.Create(wbDataPath + 'MyPlugin.esp', fmOpenRead);
    try
      ms.CopyFrom(fs, fs.Size);
    finally
      fs.Free;
    end;

    // Read header
    ms.Position := 0;
    ms.ReadBuffer(signature, 4);
    AddMessage('Signature: ' + signature);

    // Read FormID
    ms.ReadBuffer(formID, 4);
    AddMessage(Format('FormID: %s', [IntToHex(formID, 8)]));

    // Read flags
    ms.ReadBuffer(flags, 2);
    AddMessage(Format('Flags: %s', [IntToHex(flags, 4)]));

  finally
    ms.Free;
  end;
end;
```

### Example 4: Multi-File Comparison

```pascal
// Compare EditorIDs across multiple files
var
  fileLists: array of TStringList;
  i, j, fileCount: Integer;
  rec: IwbMainRecord;
begin
  fileCount := FileCount();
  SetLength(fileLists, fileCount);

  try
    // Collect EditorIDs from each file
    for i := 0 to fileCount - 1 do begin
      fileLists[i] := TStringList.Create;
      fileLists[i].Sorted := True;
      fileLists[i].Duplicates := dupIgnore;

      for j := 0 to RecordCount(FileByIndex(i)) - 1 do begin
        rec := RecordByIndex(FileByIndex(i), j);
        fileLists[i].Add(EditorID(rec));
      end;

      AddMessage(Format('%s: %d EditorIDs',
        [GetFileName(FileByIndex(i)), fileLists[i].Count]));
    end;

    // Find EditorIDs unique to first file
    if fileCount > 1 then begin
      fileLists[0].Difference(fileLists[1]);
      AddMessage(Format('Unique to %s: %d',
        [GetFileName(FileByIndex(0)), fileLists[0].Count]));
    end;

  finally
    // Clean up
    for i := 0 to fileCount - 1 do
      fileLists[i].Free;
  end;
end;
```

---

[← Back to Standard Library Overview](stdlib_home.md) | [← Previous: Graphics & Drawing](stdlib_graphics.md)
