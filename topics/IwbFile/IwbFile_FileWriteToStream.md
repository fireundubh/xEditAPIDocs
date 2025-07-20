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

## Example

```pascal
fs := TFileStream.Create(aFileName, fmCreate);
try
  FileWriteToStream(f, fs, False);
finally
  fs.Free;
end;
```
