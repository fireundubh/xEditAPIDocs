# TdfElement.LoadFromFile

## Syntax

```pascal
procedure LoadFromFile(const aFileName: string);
```

Access via: `element.LoadFromFile(FileName)`

## Description

Loads binary data into this element by reading and deserializing from a file.

The LoadFromFile method reads the entire contents of the specified file and parses it according to the element's definition structure. This is the most common way to load binary format files (NIF, BGSM, BGEM, DDS, etc.) into a structured element tree.

The file is opened and parsed from its bytes. Any existing data in the element is replaced with the newly loaded data.

If the file does not exist or cannot be read, an exception is raised.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileName | string | Full path to the binary file to load |

## Returns

This method does not return a value.

## Example

```pascal
var
    nifFile: TwbNifFile;
    headerVersion: TdfElement;
    filePath: string;
begin
    nifFile := TwbNifFile.Create;
    try
        filePath := 'C:\Games\Skyrim\Data\Meshes\Actors\Character\Character.nif';
        nifFile.LoadFromFile(filePath);

        headerVersion := nifFile.Elements['Header\Version'];
        if Assigned(headerVersion) then
            AddMessage('NIF Version: ' + headerVersion.EditValue);
        AddMessage('Block Count: ' + IntToStr(nifFile.BlocksCount));
    finally
        nifFile.Free;
    end;
end;
```

## See Also

- [TdfElement.LoadFromData](TdfElement_LoadFromData.md)
- [TdfElement.LoadFromResource](TdfElement_LoadFromResource.md)
- [TdfElement.SaveToFile](TdfElement_SaveToFile.md)
- [TdfElement.LoadFromJSONFile](TdfElement_LoadFromJSONFile.md)
