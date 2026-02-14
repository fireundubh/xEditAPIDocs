# ResourceCopy

## Syntax

```pascal
procedure ResourceCopy(AContainerName: String; AFileName: String; APathOut: String);
```

## Description

Copies the resource matching `AFileName` in the resource container `AContainerName` to `APathOut`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerName | String | The name of the resource container to copy from |
| AFileName | String | The name of the file within the container to copy |
| APathOut | String | The destination path to copy the resource to |

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

