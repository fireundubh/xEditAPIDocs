# Constants Reference

This document provides a comprehensive reference for all constants available in xEdit's JvInterpreter scripting environment.

## Table of Contents

- [TGameMode](#-tgamemode) - Game identification
- [TwbElementType](#-twbelementtype) - Element type classification
- [TwbElementState](#-twbelementstate) - Element state flags
- [TwbDefType](#-twbdeftype) - Definition types
- [TConflictThis](#-tconflictthis) - Individual record conflict status
- [TConflictAll](#-tconflictall) - Combined conflict status
- [TwbContainerState](#-twbcontainerstate) - Container initialization state
- [TGameResourceType](#-tgameresourcetype) - Resource classification
- [TdfDataType](#-tdfdatatype) - Binary data types (DF adapter)
- [TwbNifOption](#-twbnifoption) - NIF file processing options
- [TwbNifVersion](#-twbnifversion) - NIF file versions

---

## TGameMode

Game identification constants used to detect which game is currently loaded. Use with the global `wbGameMode` variable.

### Values

| Constant | Value | Game |
|----------|-------|------|
| `gmTES3` | 0 | The Elder Scrolls III: Morrowind |
| `gmTES4` | 1 | The Elder Scrolls IV: Oblivion |
| `gmTES4R` | 2 | The Elder Scrolls IV: Oblivion (Runtime) |
| `gmTES5` | 3 | The Elder Scrolls V: Skyrim |
| `gmTES5VR` | 4 | The Elder Scrolls V: Skyrim VR |
| `gmFO3` | 5 | Fallout 3 |
| `gmFNV` | 6 | Fallout: New Vegas |
| `gmFO4` | 7 | Fallout 4 |
| `gmFO4VR` | 8 | Fallout 4 VR |
| `gmFO76` | 9 | Fallout 76 |
| `gmSSE` | 10 | The Elder Scrolls V: Skyrim Special Edition |
| `gmEnderal` | 11 | Enderal: Forgotten Stories |
| `gmEnderalSE` | 12 | Enderal: Forgotten Stories Special Edition |
| `gmSF1` | 13 | Starfield |

### Example Usage

```pascal
// Example 1: Check if we're running in Skyrim Special Edition
begin
  if wbGameMode = gmSSE then
    AddMessage('Running in Skyrim Special Edition');
end;

// Example 2: Game-specific logic
begin
  case wbGameMode of
    gmTES5, gmSSE, gmTES5VR: begin
      AddMessage('This is a Skyrim variant');
    end;
    gmFO4, gmFO4VR: begin
      AddMessage('This is Fallout 4');
    end;
    gmSF1: begin
      AddMessage('This is Starfield');
    end;
  else
    AddMessage('Other game detected');
  end;
end;

// Example 3: Game-specific file extension
var
  fileExt: string;
begin
  case wbGameMode of
    gmTES3: fileExt := '.ess';
    gmTES4, gmFO3, gmFNV: fileExt := '.fos';
    gmTES5, gmSSE, gmTES5VR: fileExt := '.ess';
    gmFO4, gmFO4VR, gmFO76: fileExt := '.fos';
    gmSF1: fileExt := '.sfs';
  else
    fileExt := '.unknown';
  end;

  AddMessage('Save file extension: ' + fileExt);
end;
```

---

## TwbElementType

Element type classification constants. Every element has a `ElementType` property that returns one of these values.

### Values

| Constant | Description |
|----------|-------------|
| `etFile` | Plugin file (`.esp`, `.esm`, `.esl`) |
| `etMainRecord` | Main record (WEAP, NPC_, CELL, etc.) |
| `etGroupRecord` | Group record (container for main records) |
| `etSubRecord` | Subrecord with signature (EDID, FULL, etc.) |
| `etSubRecordStruct` | Structured subrecord with multiple fields |
| `etSubRecordArray` | Array of subrecords |
| `etSubRecordUnion` | Union subrecord (variant type) |
| `etArray` | Array element |
| `etStruct` | Structured element |
| `etValue` | Primitive value (integer, float, string) |
| `etFlag` | Flag/bitfield value |
| `etStringListTerminator` | String list terminator marker |
| `etUnion` | Union element (variant type) |
| `etStructChapter` | Chapter divider in structured element |

### Example Usage

```pascal
// Example 1: Type-specific element processing
var
  container: IwbContainer;
  i: Integer;
  element: IwbElement;
  elemType: Integer;
begin
  if Assigned(e) then begin
    container := e;
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        elemType := ElementType(element);
        case elemType of
          etMainRecord:
            AddMessage('Main record: ' + Name(element));
          etSubRecord:
            AddMessage('  Subrecord: ' + Name(element) + ' = ' + GetEditValue(element));
          etArray:
            AddMessage('  Array with ' + IntToStr(ElementCount(element)) + ' elements');
          etValue:
            AddMessage('  Value: ' + GetEditValue(element));
        end;
      end;
    end;
  end;
end;

// Example 2: Filter processing to main records only
var
  i: Integer;
  rec: IwbMainRecord;
begin
  for i := 0 to FileCount - 1 do begin
    rec := FileByIndex(i);
    if Assigned(rec) and (ElementType(rec) = etMainRecord) then
      AddMessage('Main record: ' + EditorID(rec));
  end;
end;

// Example 3: Check if element is a container type
var
  element: IwbElement;
  elemType: Integer;
begin
  element := ElementByPath(e, 'KWDA');
  if Assigned(element) then begin
    elemType := ElementType(element);
    if elemType in [etArray, etStruct, etSubRecordStruct] then
      AddMessage('Element is a container type')
    else
      AddMessage('Element is not a container');
  end;
end;
```

---

## TwbElementState

Element state flags representing various states an element can be in. Multiple states can be combined.

### Values

| Constant | Description |
|----------|-------------|
| `esModified` | Element has been modified |
| `esInternalModified` | Element internally modified (computed values changed) |
| `esUnsaved` | Element has unsaved changes |
| `esSortKeyValid` | Sort key is currently valid |
| `esExtendedSortKeyValid` | Extended sort key is valid |
| `esHidden` | Element is hidden |
| `esParentHidden` | Parent element is hidden |
| `esParentHiddenChecked` | Parent hidden state has been checked |
| `esNotReachable` | Element is not reachable (unreferenced) |
| `esReachable` | Element is reachable (referenced) |
| `esTagged` | Element is tagged/marked |
| `esResolving` | Element is being resolved |
| `esNotSuitableToAddTo` | Element cannot have children added |

### Example Usage

```pascal
// Example 1: Check if element is modified
var
  element: IwbElement;
  states: TwbElementStates;
begin
  if Assigned(element) then begin
    states := GetElementStates(element);
    if esModified in states then
      AddMessage('Element has been modified');
  end;
end;

// Example 2: Check multiple states
var
  rec: IwbMainRecord;
  states: TwbElementStates;
begin
  if Assigned(rec) then begin
    states := GetElementStates(rec);

    if esHidden in states then
      AddMessage('Record is hidden')
    else
      AddMessage('Record is visible');

    if esUnsaved in states then
      AddMessage('Warning: Unsaved changes detected');

    if esModified in states then
      AddMessage('Record has been modified');
  end;
end;

// Example 3: Check reachability (for cleaning)
var
  i: Integer;
  rec: IwbMainRecord;
  states: TwbElementStates;
  unreachableCount: Integer;
begin
  unreachableCount := 0;
  for i := 0 to RecordCount(f) - 1 do begin
    rec := RecordByIndex(f, i);
    if Assigned(rec) then begin
      states := GetElementStates(rec);
      if esNotReachable in states then begin
        Inc(unreachableCount);
        AddMessage('Unreachable: ' + EditorID(rec));
      end;
    end;
  end;
  AddMessage(Format('Total unreachable records: %d', [unreachableCount]));
end;
```

---

## TwbDefType

Definition type constants identifying the type of a definition (schema).

### Values

| Constant | Description |
|----------|-------------|
| `dtRecord` | Record definition |
| `dtSubRecord` | Subrecord definition |
| `dtSubRecordArray` | Subrecord array definition |
| `dtSubRecordStruct` | Subrecord struct definition |
| `dtSubRecordUnion` | Subrecord union definition |
| `dtString` | String value definition |
| `dtLString` | Localized string definition |
| `dtLenString` | Length-prefixed string definition |
| `dtByteArray` | Byte array definition |
| `dtInteger` | Integer value definition |
| `dtIntegerFormater` | Formatted integer definition |
| `dtFloat` | Float value definition |
| `dtArray` | Array definition |
| `dtStruct` | Struct definition |
| `dtUnion` | Union definition |
| `dtEmpty` | Empty definition (placeholder) |
| `dtStructChapter` | Struct chapter/divider definition |

### Example Usage

```pascal
// Example 1: Check definition type
var
  element: IwbElement;
  def: IwbDef;
  defType: Integer;
begin
  if Assigned(element) then begin
    def := Def(element);
    if Assigned(def) then begin
      defType := DefType(def);
      case defType of
        dtInteger: AddMessage('This is an integer field');
        dtFloat: AddMessage('This is a float field');
        dtString, dtLString: AddMessage('This is a string field');
        dtArray: AddMessage('This is an array');
        dtStruct: AddMessage('This is a structure');
      end;
    end;
  end;
end;

// Example 2: Filter for numeric fields
var
  container: IwbContainer;
  i: Integer;
  element: IwbElement;
  def: IwbDef;
  defType: Integer;
begin
  if Assigned(e) then begin
    container := e;
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        def := Def(element);
        if Assigned(def) then begin
          defType := DefType(def);
          if defType in [dtInteger, dtFloat] then
            AddMessage('Numeric field: ' + Name(element) + ' = ' + GetEditValue(element));
        end;
      end;
    end;
  end;
end;

// Example 3: Find localized strings
var
  container: IwbContainer;
  i: Integer;
  element: IwbElement;
  def: IwbDef;
begin
  if Assigned(e) then begin
    container := e;
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        def := Def(element);
        if Assigned(def) and (DefType(def) = dtLString) then
          AddMessage('Localized string: ' + Name(element));
      end;
    end;
  end;
end;
```

---

## TConflictThis

Conflict classification for an individual record's relationship to its master.

### Values

| Constant | Description |
|----------|-------------|
| `ctUnknown` | Conflict status unknown |
| `ctIgnored` | Record is ignored (filtered out) |
| `ctNotDefined` | Conflict not yet determined |
| `ctIdenticalToMaster` | Override is identical to master (ITM) |
| `ctOnlyOne` | Only one version exists (no conflict) |
| `ctHiddenByModGroup` | Hidden by mod group settings |
| `ctMaster` | This is the master record |
| `ctConflictBenign` | Benign/harmless conflict |
| `ctOverride` | Clean override (intentional change) |
| `ctIdenticalToMasterWinsConflict` | ITM that wins conflict resolution |
| `ctConflictWins` | Conflicting record that wins |
| `ctConflictLoses` | Conflicting record that loses |

### Example Usage

```pascal
// Example 1: Check if record is an ITM (Identical To Master)
var
  rec: IwbMainRecord;
  conflictThis: Integer;
begin
  rec := WinningOverride(e);
  if Assigned(rec) then begin
    conflictThis := ConflictThisForMainRecord(rec);
    if conflictThis = ctIdenticalToMaster then
      AddMessage('ITM detected: ' + Name(rec));
  end;
end;

// Example 2: Find records with real conflicts
var
  i: Integer;
  rec: IwbMainRecord;
  conflictThis: Integer;
begin
  for i := 0 to RecordCount(f) - 1 do begin
    rec := RecordByIndex(f, i);
    if Assigned(rec) then begin
      conflictThis := ConflictThisForMainRecord(rec);
      if conflictThis in [ctConflictWins, ctConflictLoses] then
        AddMessage('Conflict: ' + EditorID(rec));
    end;
  end;
end;

// Example 3: Skip hidden and ignored records
var
  i: Integer;
  rec: IwbMainRecord;
  conflictThis: Integer;
begin
  for i := 0 to RecordCount(f) - 1 do begin
    rec := RecordByIndex(f, i);
    if Assigned(rec) then begin
      conflictThis := ConflictThisForMainRecord(rec);
      if not (conflictThis in [ctIgnored, ctHiddenByModGroup]) then begin
        // Process record
        AddMessage('Processing: ' + EditorID(rec));
      end;
    end;
  end;
end;
```

---

## TConflictAll

Combined conflict status considering all versions of a record across all loaded plugins.

### Values

| Constant | Description |
|----------|-------------|
| `caUnknown` | Conflict status unknown |
| `caOnlyOne` | Only one version exists |
| `caNoConflict` | Multiple versions but no conflict |
| `caConflictBenign` | Benign/harmless conflict |
| `caOverride` | Clean override |
| `caConflict` | Conflict detected |
| `caConflictCritical` | Critical conflict (requires attention) |

### Example Usage

```pascal
// Example 1: Find critical conflicts
var
  rec: IwbMainRecord;
  conflictAll: Integer;
begin
  rec := WinningOverride(e);
  if Assigned(rec) then begin
    conflictAll := ConflictAllForMainRecord(rec);
    if conflictAll = caConflictCritical then
      AddMessage('CRITICAL CONFLICT: ' + EditorID(rec));
  end;
end;

// Example 2: Report conflict summary for a record
var
  rec: IwbMainRecord;
  conflictAll: Integer;
  conflictStr: string;
begin
  if Assigned(e) then begin
    conflictAll := ConflictAllForMainRecord(e);
    case conflictAll of
      caOnlyOne: conflictStr := 'No override';
      caNoConflict: conflictStr := 'Clean override';
      caConflictBenign: conflictStr := 'Benign conflict';
      caOverride: conflictStr := 'Override';
      caConflict: conflictStr := 'Conflict detected';
      caConflictCritical: conflictStr := 'CRITICAL CONFLICT!';
    else
      conflictStr := 'Unknown';
    end;
    AddMessage(EditorID(e) + ': ' + conflictStr);
  end;
end;

// Example 3: Export only conflicting records
var
  i: Integer;
  rec: IwbMainRecord;
  conflictAll: Integer;
  conflictCount: Integer;
begin
  conflictCount := 0;
  for i := 0 to RecordCount(f) - 1 do begin
    rec := RecordByIndex(f, i);
    if Assigned(rec) then begin
      conflictAll := ConflictAllForMainRecord(rec);
      if conflictAll in [caConflict, caConflictCritical] then begin
        Inc(conflictCount);
        AddMessage(Format('Conflict [%d]: %s', [conflictCount, EditorID(rec)]));
      end;
    end;
  end;
  AddMessage(Format('Total conflicts: %d', [conflictCount]));
end;
```

---

## TwbContainerState

Container initialization state flags.

### Values

| Constant | Description |
|----------|-------------|
| `csInit` | Initial state (not initialized) |
| `csInitOnce` | Initialize once only |
| `csInitDone` | Initialization complete |
| `csInitializing` | Currently initializing |
| `csRefsBuild` | Building references |
| `csAsCreatedEmpty` | Created as empty container |

### Example Usage

```pascal
// Example 1: Check if container is initialized
var
  container: IwbContainer;
  states: TwbContainerStates;
begin
  if Assigned(e) then begin
    container := e;
    states := GetContainerStates(container);
    if csInitDone in states then
      AddMessage('Container is ready')
    else
      AddMessage('Container still initializing');
  end;
end;

// Example 2: Check initialization state
var
  container: IwbContainer;
  states: TwbContainerStates;
begin
  if Assigned(e) then begin
    container := e;
    states := GetContainerStates(container);

    if csInitializing in states then
      AddMessage('Container is currently initializing')
    else if csInitDone in states then
      AddMessage('Container initialization complete')
    else if csInit in states then
      AddMessage('Container not yet initialized');
  end;
end;

// Example 3: Check if created as empty
var
  container: IwbContainer;
  states: TwbContainerStates;
begin
  if Assigned(e) then begin
    container := e;
    states := GetContainerStates(container);
    if csAsCreatedEmpty in states then
      AddMessage('Container was created empty (new record)');
  end;
end;
```

---

## TGameResourceType

Resource type classification for game assets.

### Values

| Constant | Description |
|----------|-------------|
| `resMesh` | 3D mesh/model files (NIF) |
| `resTexture` | Texture files (DDS, TGA) |
| `resSound` | Sound effect files (WAV, XWM) |
| `resMusic` | Music files |
| `resMaterial` | Material definition files (BGSM, BGEM) |

### Example Usage

```pascal
// Example 1: Get all mesh resources from a record
var
  rec: IwbMainRecord;
  resources: TStringList;
  i: Integer;
begin
  if Assigned(e) then begin
    resources := TStringList.Create;
    try
      GetResources(e, resources, resMesh);

      AddMessage(Format('Found %d meshes:', [resources.Count]));
      for i := 0 to resources.Count - 1 do
        AddMessage('  Mesh: ' + resources[i]);
    finally
      resources.Free;
    end;
  end;
end;

// Example 2: Get all textures from a record
var
  rec: IwbMainRecord;
  resources: TStringList;
  i: Integer;
begin
  if Assigned(e) then begin
    resources := TStringList.Create;
    try
      GetResources(e, resources, resTexture);
      AddMessage(Format('%s uses %d textures', [EditorID(e), resources.Count]));

      for i := 0 to resources.Count - 1 do
        AddMessage('  ' + resources[i]);
    finally
      resources.Free;
    end;
  end;
end;

// Example 3: Get all resource types from a record
var
  rec: IwbMainRecord;
  resources: TStringList;
  resType: Integer;
  typeNames: array[0..4] of string;
begin
  if Assigned(e) then begin
    typeNames[0] := 'Mesh';
    typeNames[1] := 'Texture';
    typeNames[2] := 'Sound';
    typeNames[3] := 'Music';
    typeNames[4] := 'Material';

    resources := TStringList.Create;
    try
      for resType := resMesh to resMaterial do begin
        resources.Clear;
        GetResources(e, resources, resType);
        if resources.Count > 0 then
          AddMessage(Format('%s: %d %s(s)',
            [EditorID(e), resources.Count, typeNames[resType]]));
      end;
    finally
      resources.Free;
    end;
  end;
end;
```

---

## TdfDataType

Binary data types used by the DF (Data Format) adapter for NIF files, materials, and other binary formats.

### Values

| Constant | Description |
|----------|-------------|
| `dftNone` | No data type |
| `dftStruct` | Structure (composite type) |
| `dftArray` | Array of elements |
| `dftUnion` | Union (variant type) |
| `dftMerge` | Merged elements |
| `dftBytes` | Raw byte array |
| `dftChars` | Character array (string) |
| `dftU8` | Unsigned 8-bit integer (0..255) |
| `dftS8` | Signed 8-bit integer (-128..127) |
| `dftU16` | Unsigned 16-bit integer (0..65535) |
| `dftS16` | Signed 16-bit integer (-32768..32767) |
| `dftU32` | Unsigned 32-bit integer |
| `dftS32` | Signed 32-bit integer |
| `dftU64` | Unsigned 64-bit integer |
| `dftS64` | Signed 64-bit integer |
| `dftFloat16` | 16-bit floating point (half precision) |
| `dftFloat32` | 32-bit floating point (single precision) |

### Example Usage

```pascal
// Example 1: Check data type of DF element
var
  nif: TwbNifFile;
  block: TwbNifBlock;
  element: TdfElement;
  dataType: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\test.nif');
    block := nif.Blocks[0];

    element := block.Elements[0];
    dataType := element.DataType;

    case dataType of
      dftU8, dftU16, dftU32, dftU64:
        AddMessage('Unsigned integer: ' + element.EditValue);
      dftS8, dftS16, dftS32, dftS64:
        AddMessage('Signed integer: ' + element.EditValue);
      dftFloat16, dftFloat32:
        AddMessage('Float: ' + element.EditValue);
      dftStruct:
        AddMessage('Structure with ' + IntToStr(element.Count) + ' fields');
      dftArray:
        AddMessage('Array with ' + IntToStr(element.Count) + ' elements');
    end;
  finally
    nif.Free;
  end;
end;

// Example 2: Find all float values in a NIF block
var
  nif: TwbNifFile;
  block: TwbNifBlock;
  i: Integer;
  element: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\test.nif');
    block := nif.Blocks[0];

    for i := 0 to block.Count - 1 do begin
      element := block.Elements[i];
      if element.DataType = dftFloat32 then
        AddMessage(element.Name + ' = ' + element.EditValue);
    end;
  finally
    nif.Free;
  end;
end;

// Example 3: Type-based validation
var
  element: TdfElement;
  dataType: Integer;
  value: string;
begin
  dataType := element.DataType;

  // Validate based on type
  if dataType in [dftU8, dftU16, dftU32] then begin
    value := element.EditValue;
    if StrToIntDef(value, -1) < 0 then
      AddMessage('Warning: Negative value in unsigned field');
  end else if dataType in [dftFloat16, dftFloat32] then begin
    AddMessage('Float precision: ' + element.EditValue);
  end;
end;
```

---

## TwbNifOption

NIF file processing options that control how NIF files are loaded and saved.

### Values

| Constant | Description |
|----------|-------------|
| `nfoCollapseLinkArrays` | Collapse NIF link arrays for compact representation |
| `nfoRemoveUnusedStrings` | Remove unused strings from NIF string table |

### Example Usage

```pascal
// Example 1: Create NIF file with optimizations
var
  nif: TwbNifFile;
  options: TwbNifOptions;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\architecture\building.nif');

    // Get current options
    options := nif.Options;

    // Enable optimizations
    options := options + [nfoCollapseLinkArrays, nfoRemoveUnusedStrings];
    nif.Options := options;

    // Save optimized version
    nif.SaveToFile('meshes\architecture\building_optimized.nif');
    AddMessage('Saved optimized NIF with collapsed arrays and removed unused strings');
  finally
    nif.Free;
  end;
end;

// Example 2: Check if option is enabled
var
  nif: TwbNifFile;
  options: TwbNifOptions;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\test.nif');

    options := nif.Options;
    if nfoRemoveUnusedStrings in options then
      AddMessage('Unused strings will be removed on save');

    if nfoCollapseLinkArrays in options then
      AddMessage('Link arrays will be collapsed');
  finally
    nif.Free;
  end;
end;

// Example 3: Batch optimize NIF files
var
  nif: TwbNifFile;
  files: TStringList;
  i: Integer;
  fileName: string;
begin
  files := TStringList.Create;
  try
    // Get list of NIF files
    files.Add('meshes\clutter\item01.nif');
    files.Add('meshes\clutter\item02.nif');

    for i := 0 to files.Count - 1 do begin
      fileName := files[i];
      nif := TwbNifFile.Create;
      try
        nif.LoadFromFile(fileName);

        // Enable all optimizations
        nif.Options := [nfoCollapseLinkArrays, nfoRemoveUnusedStrings];

        nif.SaveToFile(fileName);
        AddMessage('Optimized: ' + fileName);
      finally
        nif.Free;
      end;
    end;
  finally
    files.Free;
  end;
end;
```

---

## TwbNifVersion

NIF file version constants corresponding to different game engines.

### Values

| Constant | Value | Game | Engine Version |
|----------|-------|------|----------------|
| `nfTES3` | 1 | Morrowind | NetImmerse |
| `nfTES4` | 2 | Oblivion | Gamebryo |
| `nfFO3` | 3 | Fallout 3, Fallout: New Vegas | Gamebryo |
| `nfTES5` | 4 | Skyrim, Skyrim Legendary Edition | Creation Engine |
| `nfSSE` | 5 | Skyrim Special Edition | Creation Engine (64-bit) |
| `nfFO4` | 6 | Fallout 4 | Creation Engine |

### Example Usage

```pascal
// Example 1: Load and convert NIF to Skyrim SE format
var
  nif: TwbNifFile;
  version: Integer;
  versionName: string;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\oldformat.nif');

    // Check current version
    version := nif.NifVersion;
    case version of
      nfTES3: versionName := 'Morrowind';
      nfTES4: versionName := 'Oblivion';
      nfFO3: versionName := 'Fallout 3/NV';
      nfTES5: versionName := 'Skyrim LE';
      nfSSE: versionName := 'Skyrim SE';
      nfFO4: versionName := 'Fallout 4';
    else
      versionName := 'Unknown';
    end;

    AddMessage('Current format: ' + versionName);

    // Convert to Skyrim SE if needed
    if version <> nfSSE then begin
      AddMessage('Converting to Skyrim SE format...');
      nif.NifVersion := nfSSE;
      nif.SaveToFile('meshes\converted.nif');
      AddMessage('Conversion complete');
    end;
  finally
    nif.Free;
  end;
end;

// Example 2: Create new NIF for current game
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    // Set version based on current game
    case wbGameMode of
      gmTES5, gmTES5VR: nif.NifVersion := nfTES5;
      gmSSE, gmEnderal, gmEnderalSE: nif.NifVersion := nfSSE;
      gmFO4, gmFO4VR: nif.NifVersion := nfFO4;
    else
      raise Exception.Create('Unsupported game for NIF creation');
    end;

    // Create root node
    rootNode := nif.AddBlock('BSFadeNode');
    rootNode.ElementByPath['Name'].EditValue := 'Scene Root';

    nif.SaveToFile('meshes\test\new_mesh.nif');
    AddMessage('Created NIF for ' + wbGameName);
  finally
    nif.Free;
  end;
end;

// Example 3: Batch version check
var
  files: TStringList;
  i: Integer;
  nif: TwbNifFile;
  version: Integer;
  stats: array[nfTES3..nfFO4] of Integer;
  v: Integer;
begin
  // Initialize counters
  for v := nfTES3 to nfFO4 do
    stats[v] := 0;

  files := TStringList.Create;
  try
    files.Add('meshes\armor\iron\cuirass.nif');
    files.Add('meshes\armor\iron\gauntlets.nif');

    for i := 0 to files.Count - 1 do begin
      nif := TwbNifFile.Create;
      try
        nif.LoadFromFile(files[i]);
        version := nif.NifVersion;
        if (version >= nfTES3) and (version <= nfFO4) then
          Inc(stats[version]);
      finally
        nif.Free;
      end;
    end;

    AddMessage('NIF Version Statistics:');
    AddMessage('  Morrowind: ' + IntToStr(stats[nfTES3]));
    AddMessage('  Oblivion: ' + IntToStr(stats[nfTES4]));
    AddMessage('  Fallout 3/NV: ' + IntToStr(stats[nfFO3]));
    AddMessage('  Skyrim LE: ' + IntToStr(stats[nfTES5]));
    AddMessage('  Skyrim SE: ' + IntToStr(stats[nfSSE]));
    AddMessage('  Fallout 4: ' + IntToStr(stats[nfFO4]));
  finally
    files.Free;
  end;
end;
```

---

## See Also

- [Glossary](Glossary.md) - Terminology definitions
- [Global Functions](README.md) - Available script functions
- Element property documentation for using these constants with actual elements
