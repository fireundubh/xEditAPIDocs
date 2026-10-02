# FileWriteToStream

## Syntax

```pascal
procedure FileWriteToStream(AFile: IwbFile; AStream: TStream; AResetModified: Integer);
```

## Description

Writes the plugin in `AFile` to `AStream`.

`AResetModified` is required:

| Value | Effect |
|-------|--------|
| 0 | Leave the modified state as it is |
| 2 | If the file is modified, set the internal modified flag. The modified flag stays set |
| any other integer | Clear the modified state |

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to write |
| AStream | TStream | The stream to write to |
| AResetModified | Integer | How to treat the modified state after the write |

## Returns

Returns nothing.

## Example

```pascal
var
  f: IwbFile;
  fs: TFileStream;
begin
  f := FileByIndex(0);
  if Assigned(f) then begin
    fs := TFileStream.Create('C:\Temp\out.esp', fmCreate);
    try
      FileWriteToStream(f, fs, 1);
    finally
      fs.Free;
    end;
  end;
end;
```

## See Also

- [GetFileName](IwbFile_GetFileName.md)
