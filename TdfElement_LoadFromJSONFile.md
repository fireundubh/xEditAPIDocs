# TdfElement.LoadFromJSONFile

## Syntax

```pascal
procedure LoadFromJSONFile(const aFileName: string);
```

## Description

Loads element data from a JSON file by reading and deserializing the JSON structure.

The LoadFromJSONFile method reads a JSON file and populates this element with the data it contains. The JSON structure must match the element's definition - field names should correspond to element names, and nested objects should match the hierarchy.

This is useful for working with human-readable representations of binary files, allowing you to edit complex structures in JSON format and then convert them back to binary. It's commonly used in asset conversion workflows or for debugging binary file structures.

Any existing data in the element is replaced with the newly loaded data.

If the file does not exist, cannot be read, or contains invalid JSON, an exception is raised.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileName | string | Full path to the JSON file to load |

## Returns

This method does not return a value.

## Example

```pascal
var
    materialFile: TwbBGSMFile;
    jsonPath: string;
begin
    materialFile := TwbBGSMFile.Create;
    try
        jsonPath := 'C:\Temp\material_export.json';

        // Load from JSON
        materialFile.LoadFromJSONFile(jsonPath);

        // Access data
        AddMessage('Diffuse Texture: ' + materialFile.Elements['Diffuse Texture'].EditValue);
    finally
        materialFile.Free;
    end;
end;
```

## See Also

- [TdfElement.LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement.SaveToJSONFile](TdfElement_SaveToJSONFile.md)
- [TdfElement.FromJSON](TdfElement_FromJSON.md)
- [TdfElement.ToJSON](TdfElement_ToJSON.md)
