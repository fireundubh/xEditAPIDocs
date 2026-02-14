# FileWriteToStream

## Syntax

```pascal
procedure FileWriteToStream(AFile: IwbFile; AStream: TStream; AResetModified: Integer = 1);
```

## Description

Writes the contents of `AFile` to `AStream`

If `AResetModified` is...

| Arg | Description     |
|:----|:----------------|
| `0` | `rmNo`          |
| `1` | `rmYes`         |
| `2` | `rmSetInternal` |

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to write to the stream |
| AStream | TStream | The stream to write the file contents to |
| AResetModified | Integer | Reset modified flag (0=rmNo, 1=rmYes, 2=rmSetInternal, defaults to 1) |

## Example

```pascal
fs := TFileStream.Create(aFileName, fmCreate);
try
  FileWriteToStream(f, fs, False);
finally
  fs.Free;
end;
```

