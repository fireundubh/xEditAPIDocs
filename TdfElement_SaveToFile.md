# TdfElement.SaveToFile

## Syntax

```pascal
procedure SaveToFile(const aFileName: string);
```

## Description

Serializes this element to binary format and writes it to a file.

The SaveToFile method converts the element tree structure back to its binary representation and writes it to the specified file path. This is the primary way to export modified binary format files (NIF, BGSM, BGEM, DDS, etc.) after making changes through the element API.

The element tree is serialized depth-first, with each element writing its data according to its definition. Only enabled elements are included in the output.

If the file already exists, it will be overwritten. If the directory path does not exist or the file cannot be written, an exception is raised.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileName | string | Full path where the binary file should be saved |

## Returns

This method does not return a value.

## Example

```pascal
var
    nifFile: TwbNifFile;
    inputPath, outputPath: string;
begin
    nifFile := TwbNifFile.Create;
    try
        inputPath := 'C:\Games\Skyrim\Data\Meshes\test.nif';
        outputPath := 'C:\Temp\modified_test.nif';

        // Load, modify, and save
        nifFile.LoadFromFile(inputPath);
        nifFile.Elements['Header\Creator'].EditValue := 'xEdit Script';

        nifFile.SaveToFile(outputPath);
        AddMessage('Saved modified NIF to: ' + outputPath);
    finally
        nifFile.Free;
    end;
end;
```

## See Also

- [TdfElement.LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement.SaveToJSONFile](TdfElement_SaveToJSONFile.md)
- [TdfElement.DataSize](TdfElement_DataSize.md)
- [TdfElement.ToJSON](TdfElement_ToJSON.md)
