# ResourceCopy

## Syntax

```pascal
procedure ResourceCopy(AContainerName: String; AFileName: String; APathOut: String);
```

## Description

Copies the resource matching `AFileName` in the resource container `AContainerName` to `APathOut`

## Example

```pascal
f := TempPath + ExtractFileName(aFileName);
try
  ResourceCopy(aContainerName, aFileName, f);
except
  on E: Exception do begin
    MessageDlg(E.Message, mtError, [mbOk], 0);
    Exit;
  end;
end;
```
