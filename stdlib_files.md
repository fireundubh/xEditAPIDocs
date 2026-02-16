# File & Path Operations Reference

Functions for file I/O, path manipulation, directory operations, and stream-based data handling.

**Units:** SysUtils, Classes

[← Back to Standard Library Overview](stdlib_home.md)

## Table of Contents

- [File Existence and Properties](#file-existence-and-properties)
- [File I/O (Low-Level)](#file-io-low-level)
- [File Operations](#file-operations)
- [Path Functions](#path-functions)
- [Directory Operations](#directory-operations)
- [File Search](#file-search)
- [Stream Classes](#stream-classes)
- [TStringList File Operations](#tstringlist-file-operations)

## File Existence and Properties

| Function | Signature | Description |
|----------|-----------|-------------|
| `FileExists` | `FileExists(FileName: string): Boolean` | Check if file exists |
| `DirectoryExists` | `DirectoryExists(Dir: string): Boolean` | Check if directory exists |
| `FileAge` | `FileAge(FileName: string): Integer` | Get file date/time as integer |
| `FileGetAttr` | `FileGetAttr(FileName: string): Integer` | Get file attributes (readonly, hidden, etc.) |
| `FileSetAttr` | `FileSetAttr(FileName: string, Attr: Integer): Integer` | Set file attributes |
| `FileSize` | `FileSize(FileName: string): Int64` | Get file size in bytes |

### File Attribute Constants

```pascal
faReadOnly  = $00000001;  // Read-only file
faHidden    = $00000002;  // Hidden file
faSysFile   = $00000004;  // System file
faDirectory = $00000010;  // Directory
faArchive   = $00000020;  // Archive bit
```

### xEdit Example: Check Plugin File
```pascal
// Verify plugin file before processing
var
  pluginPath: string;
  fileSize: Int64;
  attr: Integer;
begin
  pluginPath := wbDataPath + 'Skyrim.esm';

  if not FileExists(pluginPath) then begin
    AddMessage('ERROR: File not found: ' + pluginPath);
    Exit;
  end;

  fileSize := FileSize(pluginPath);
  AddMessage(Format('File size: %d bytes (%.2f MB)', [fileSize, fileSize / 1048576]));

  attr := FileGetAttr(pluginPath);
  if (attr and faReadOnly) <> 0 then
    AddMessage('WARNING: File is read-only');
end;
```

## File I/O (Low-Level)

Low-level file operations using handles. For easier file handling, use [Stream Classes](#stream-classes) or [TStringList](#tstringlist-file-operations).

| Function | Signature | Description |
|----------|-----------|-------------|
| `FileOpen` | `FileOpen(FileName: string, Mode: LongWord): Integer` | Open file, returns handle |
| `FileCreate` | `FileCreate(FileName: string): Integer` | Create file, returns handle |
| `FileRead` | `FileRead(Handle: Integer, var Buffer, Count: Cardinal): Integer` | Read bytes from file |
| `FileWrite` | `FileWrite(Handle: Integer, const Buffer, Count: Cardinal): Integer` | Write bytes to file |
| `FileSeek` | `FileSeek(Handle: Integer, Offset, Origin: Integer): Integer` | Move file pointer |
| `FileClose` | `FileClose(Handle: Integer)` | Close file handle |

### File Open Mode Constants

```pascal
fmOpenRead       = $0000;  // Read-only
fmOpenWrite      = $0001;  // Write-only
fmOpenReadWrite  = $0002;  // Read and write
fmShareDenyNone  = $0040;  // Allow others to access
```

### File Seek Origin Constants

```pascal
soFromBeginning = 0;  // Seek from start of file
soFromCurrent   = 1;  // Seek from current position
soFromEnd       = 2;  // Seek from end of file
```

### Example: Read Binary Data
```pascal
var
  Handle: Integer;
  Buffer: array[0..255] of Byte;
  BytesRead: Integer;
begin
  Handle := FileOpen('data.bin', fmOpenRead);
  if Handle = -1 then begin
    AddMessage('ERROR: Could not open file');
    Exit;
  end;

  try
    BytesRead := FileRead(Handle, Buffer, SizeOf(Buffer));
    AddMessage(Format('Read %d bytes', [BytesRead]));
  finally
    FileClose(Handle);
  end;
end;
```

**Note:** For most use cases, [TFileStream](#tfilestream) is easier to use than low-level file functions.

## File Operations

| Function | Signature | Description |
|----------|-----------|-------------|
| `DeleteFile` | `DeleteFile(FileName: string): Boolean` | Delete file (returns True on success) |
| `RenameFile` | `RenameFile(OldName, NewName: string): Boolean` | Rename/move file |
| `CopyFile` | `CopyFile(Source, Dest: PChar, FailIfExists: Boolean): Boolean` | Copy file (Windows API) |

### xEdit Example: Backup Plugin File
```pascal
// Create backup of plugin before modification
function BackupPlugin(const fileName: string): Boolean;
var
  sourcePath, backupPath: string;
  timeStamp: string;
begin
  Result := False;
  sourcePath := wbDataPath + fileName;

  if not FileExists(sourcePath) then begin
    AddMessage('ERROR: Source file not found: ' + sourcePath);
    Exit;
  end;

  // Create timestamped backup
  timeStamp := FormatDateTime('yyyymmdd_hhnnss', Now());
  backupPath := ChangeFileExt(sourcePath, Format('.%s.backup', [timeStamp]));

  if CopyFile(PChar(sourcePath), PChar(backupPath), False) then begin
    AddMessage('Backup created: ' + backupPath);
    Result := True;
  end else
    AddMessage('ERROR: Failed to create backup');
end;
```

## Path Functions

Functions for manipulating file paths and names.

| Function | Signature | Description |
|----------|-----------|-------------|
| `ExtractFilePath` | `ExtractFilePath(FileName: string): string` | Get path with trailing delimiter (e.g., 'C:\Dir\') |
| `ExtractFileDir` | `ExtractFileDir(FileName: string): string` | Get directory without trailing delimiter (e.g., 'C:\Dir') |
| `ExtractFileName` | `ExtractFileName(FileName: string): string` | Get filename with extension (e.g., 'file.txt') |
| `ExtractFileExt` | `ExtractFileExt(FileName: string): string` | Get extension with dot (e.g., '.txt') |
| `ExtractFileDrive` | `ExtractFileDrive(FileName: string): string` | Get drive letter (e.g., 'C:') |
| `ChangeFileExt` | `ChangeFileExt(FileName, Extension: string): string` | Replace file extension |
| `ExpandFileName` | `ExpandFileName(FileName: string): string` | Convert to full absolute path |
| `ExtractRelativePath` | `ExtractRelativePath(BaseName, DestName: string): string` | Get relative path |
| `IncludeTrailingPathDelimiter` | `IncludeTrailingPathDelimiter(Path: string): string` | Ensure path ends with '\' |
| `ExcludeTrailingPathDelimiter` | `ExcludeTrailingPathDelimiter(Path: string): string` | Remove trailing '\' |
| `IsPathDelimiter` | `IsPathDelimiter(Path: string, Index: Integer): Boolean` | Check if character is path delimiter |

### Path Constants

```pascal
PathDelim = '\';      // Windows path delimiter
DriveDelim = ':';     // Drive letter delimiter
PathSep = ';';        // Path list separator (as in PATH environment variable)
```

### xEdit Path Examples

#### Build Output File Path
```pascal
// Create output path for export
var
  rec: IwbMainRecord;
  basePath, fileName, outputPath: string;
begin
  rec := e;
  basePath := IncludeTrailingPathDelimiter(wbDataPath) + 'Output\';

  // Build filename from EditorID
  fileName := rec.EditorID + '.txt';
  outputPath := basePath + fileName;

  AddMessage('Output path: ' + outputPath);

  // Ensure directory exists
  if not DirectoryExists(basePath) then
    ForceDirectories(basePath);
end;
```

#### Parse Script Path Components
```pascal
// Extract components from script file path
var
  scriptPath, dir, name, ext: string;
begin
  scriptPath := ScriptsPath + 'Edit Scripts\MyScript.pas';

  dir := ExtractFileDir(scriptPath);        // 'C:\...\Edit Scripts'
  name := ExtractFileName(scriptPath);      // 'MyScript.pas'
  ext := ExtractFileExt(scriptPath);        // '.pas'

  AddMessage('Directory: ' + dir);
  AddMessage('Filename: ' + name);
  AddMessage('Extension: ' + ext);

  // Change extension
  outputPath := ChangeFileExt(scriptPath, '.txt');
  AddMessage('Output: ' + outputPath);      // 'MyScript.txt'
end;
```

#### Convert Relative to Absolute Path
```pascal
// Expand relative path to absolute
var
  relativePath, absolutePath: string;
begin
  relativePath := '..\Data\Skyrim.esm';
  absolutePath := ExpandFileName(relativePath);

  AddMessage('Relative: ' + relativePath);
  AddMessage('Absolute: ' + absolutePath);
end;
```

## Directory Operations

| Function | Signature | Description |
|----------|-----------|-------------|
| `GetCurrentDir` | `GetCurrentDir(): string` | Get current working directory |
| `SetCurrentDir` | `SetCurrentDir(Dir: string): Boolean` | Change working directory |
| `CreateDir` | `CreateDir(Dir: string): Boolean` | Create directory (single level) |
| `RemoveDir` | `RemoveDir(Dir: string): Boolean` | Remove directory (must be empty) |
| `ForceDirectories` | `ForceDirectories(Dir: string): Boolean` | Create directory and all parent directories |
| `DiskFree` | `DiskFree(Drive: Byte): Int64` | Free disk space in bytes (0=current, 1=A:, 3=C:) |
| `DiskSize` | `DiskSize(Drive: Byte): Int64` | Total disk size in bytes |

### xEdit Example: Create Output Directory Structure
```pascal
// Create organized output directories
var
  baseDir, recordsDir, reportsDir, logsDir: string;
begin
  baseDir := IncludeTrailingPathDelimiter(wbDataPath) + 'ScriptOutput';
  recordsDir := baseDir + '\Records';
  reportsDir := baseDir + '\Reports';
  logsDir := baseDir + '\Logs';

  // Create all directories at once
  if not DirectoryExists(baseDir) then begin
    if ForceDirectories(baseDir) then
      AddMessage('Created base directory: ' + baseDir)
    else begin
      AddMessage('ERROR: Could not create directory: ' + baseDir);
      Exit;
    end;
  end;

  ForceDirectories(recordsDir);
  ForceDirectories(reportsDir);
  ForceDirectories(logsDir);

  // Check disk space
  var freeSpace: Int64;
  freeSpace := DiskFree(0);  // 0 = current drive
  AddMessage(Format('Free disk space: %.2f GB', [freeSpace / 1073741824]));
end;
```

## File Search

Find files matching patterns using TSearchRec.

| Function | Signature | Description |
|----------|-----------|-------------|
| `FindFirst` | `FindFirst(Path: string, Attr: Integer, var Rec: TSearchRec): Integer` | Start file search (returns 0 on success) |
| `FindNext` | `FindNext(var Rec: TSearchRec): Integer` | Continue search (returns 0 on success) |
| `FindClose` | `FindClose(var Rec: TSearchRec)` | End search (always call this!) |

### TSearchRec Fields

```pascal
TSearchRec = record
  Name: string;           // Filename
  Size: Int64;            // File size in bytes
  Attr: Integer;          // File attributes
  TimeStamp: TDateTime;   // Last modified time
  // ... other fields
end;
```

### xEdit Example: Find All Plugin Files
```pascal
// List all ESP/ESM files in Data directory
var
  searchRec: TSearchRec;
  searchPath: string;
  count: Integer;
begin
  count := 0;
  searchPath := IncludeTrailingPathDelimiter(wbDataPath) + '*.es*';

  if FindFirst(searchPath, faAnyFile, searchRec) = 0 then begin
    try
      repeat
        if (searchRec.Attr and faDirectory) = 0 then begin
          AddMessage(Format('%s (%d bytes)', [searchRec.Name, searchRec.Size]));
          Inc(count);
        end;
      until FindNext(searchRec) <> 0;
    finally
      FindClose(searchRec);  // Always close!
    end;

    AddMessage(Format('Found %d plugin files', [count]));
  end else
    AddMessage('No plugin files found');
end;
```

### Example: Find Recently Modified Files
```pascal
// Find files modified in last 24 hours
var
  searchRec: TSearchRec;
  searchPath: string;
  cutoffTime: TDateTime;
begin
  cutoffTime := Now() - 1;  // 24 hours ago
  searchPath := IncludeTrailingPathDelimiter(wbDataPath) + '*.*';

  if FindFirst(searchPath, faAnyFile, searchRec) = 0 then begin
    try
      repeat
        if searchRec.TimeStamp >= cutoffTime then
          AddMessage(Format('%s (modified: %s)', [
            searchRec.Name,
            FormatDateTime('yyyy-mm-dd hh:nn:ss', searchRec.TimeStamp)
          ]));
      until FindNext(searchRec) <> 0;
    finally
      FindClose(searchRec);
    end;
  end;
end;
```

## Stream Classes

Stream classes provide flexible, high-level file I/O. All streams inherit from TStream.

### TStream Base Class

| Method | Signature | Description |
|--------|-----------|-------------|
| `Read` | `Read(var Buffer, Count: Longint): Longint` | Read bytes |
| `Write` | `Write(const Buffer, Count: Longint): Longint` | Write bytes |
| `Seek` | `Seek(Offset: Int64, Origin: TSeekOrigin): Int64` | Move position |
| `CopyFrom` | `CopyFrom(Source: TStream, Count: Int64): Int64` | Copy from another stream |
| **Position** | `Position: Int64` | Current position (property) |
| **Size** | `Size: Int64` | Stream size (property) |

### TFileStream

Read and write files using streams.

**Constructor:**
```pascal
TFileStream.Create(FileName: string, Mode: Word)
```

**Mode constants:**
```pascal
fmCreate        // Create new file (overwrites existing)
fmOpenRead      // Open for reading only
fmOpenWrite     // Open for writing only
fmOpenReadWrite // Open for reading and writing
```

#### Example: Write Binary Data
```pascal
var
  fs: TFileStream;
  data: array[0..99] of Byte;
  i: Integer;
begin
  // Fill array with data
  for i := 0 to 99 do
    data[i] := i;

  fs := TFileStream.Create('output.dat', fmCreate);
  try
    fs.Write(data, SizeOf(data));
    AddMessage(Format('Wrote %d bytes', [fs.Size]));
  finally
    fs.Free;
  end;
end;
```

### TMemoryStream

Work with data in memory.

| Method | Signature | Description |
|--------|-----------|-------------|
| `LoadFromFile` | `LoadFromFile(FileName: string)` | Load file into memory |
| `SaveToFile` | `SaveToFile(FileName: string)` | Save memory to file |
| `SetSize` | `SetSize(NewSize: Int64)` | Resize buffer |
| `Clear` | `Clear()` | Empty the stream |

#### Example: Load and Modify File in Memory
```pascal
var
  ms: TMemoryStream;
  data: Byte;
begin
  ms := TMemoryStream.Create;
  try
    // Load entire file into memory
    ms.LoadFromFile('input.dat');
    AddMessage(Format('Loaded %d bytes', [ms.Size]));

    // Read from memory
    ms.Position := 0;
    ms.Read(data, 1);
    AddMessage(Format('First byte: %d', [data]));

    // Modify in memory
    data := 255;
    ms.Position := 0;
    ms.Write(data, 1);

    // Save back to file
    ms.SaveToFile('output.dat');
  finally
    ms.Free;
  end;
end;
```

### TStringStream

Work with strings as streams.

**Constructor:**
```pascal
TStringStream.Create(const AString: string)
```

**Property:**
- `DataString: string` - Get/set entire string content

#### Example: Build String Using Stream
```pascal
var
  ss: TStringStream;
  line: string;
begin
  ss := TStringStream.Create('');
  try
    // Write to string stream
    line := 'Line 1' + #13#10;
    ss.WriteString(line);

    line := 'Line 2' + #13#10;
    ss.WriteString(line);

    // Get final string
    AddMessage(ss.DataString);

    // Save to file
    ss.SaveToFile('output.txt');
  finally
    ss.Free;
  end;
end;
```

### xEdit Example: Export Records to Binary Stream
```pascal
// Export record data to binary file
var
  fs: TFileStream;
  rec: IwbMainRecord;
  formID: Cardinal;
  edid: string;
  edidLen: Integer;
begin
  fs := TFileStream.Create(wbDataPath + 'records.dat', fmCreate);
  try
    for i := 0 to RecordCount(f) - 1 do begin
      rec := RecordByIndex(f, i);

      // Write FormID (4 bytes)
      formID := rec.FormID;
      fs.Write(formID, 4);

      // Write EditorID (length + string)
      edid := rec.EditorID;
      edidLen := Length(edid);
      fs.Write(edidLen, 4);
      if edidLen > 0 then
        fs.Write(PChar(edid)^, edidLen);
    end;

    AddMessage(Format('Exported %d records to binary file', [RecordCount(f)]));
  finally
    fs.Free;
  end;
end;
```

## TStringList File Operations

TStringList provides the easiest way to work with text files. See [Data Structures Reference](stdlib_data.md) for complete TStringList documentation.

| Method | Signature | Description |
|--------|-----------|-------------|
| `LoadFromFile` | `LoadFromFile(FileName: string)` | Load text file (one line per string) |
| `SaveToFile` | `SaveToFile(FileName: string)` | Save to text file |
| `LoadFromStream` | `LoadFromStream(Stream: TStream)` | Load from stream |
| `SaveToStream` | `SaveToStream(Stream: TStream)` | Save to stream |

### xEdit Example: Export EditorIDs to File
```pascal
// Export all EditorIDs to text file
var
  list: TStringList;
  i: Integer;
  rec: IwbMainRecord;
  outputPath: string;
begin
  list := TStringList.Create;
  try
    // Collect EditorIDs
    for i := 0 to RecordCount(f) - 1 do begin
      rec := RecordByIndex(f, i);
      if rec.EditorID <> '' then
        list.Add(rec.EditorID);
    end;

    // Sort alphabetically
    list.Sort;

    // Save to file
    outputPath := wbDataPath + 'EditorIDs.txt';
    list.SaveToFile(outputPath);

    AddMessage(Format('Exported %d EditorIDs to: %s', [list.Count, outputPath]));
  finally
    list.Free;
  end;
end;
```

### Example: Read Configuration File
```pascal
// Load configuration from INI-style file
var
  config: TStringList;
  i: Integer;
  line, key, value: string;
  pos: Integer;
begin
  config := TStringList.Create;
  try
    config.LoadFromFile('config.txt');

    for i := 0 to config.Count - 1 do begin
      line := Trim(config[i]);

      // Skip comments and empty lines
      if (line = '') or (Copy(line, 1, 1) = ';') then
        Continue;

      // Parse key=value
      pos := Pos('=', line);
      if pos > 0 then begin
        key := Trim(Copy(line, 1, pos - 1));
        value := Trim(Copy(line, pos + 1, Length(line)));
        AddMessage(Format('%s = %s', [key, value]));
      end;
    end;
  finally
    config.Free;
  end;
end;
```

---

[← Back to Standard Library Overview](stdlib_home.md) | [Next: Date & Time →](stdlib_datetime.md)
