# TdfElement.SaveToJSONFile

## Syntax

```pascal
procedure SaveToJSONFile(const aFileName: string; aCompact: Boolean);
```

## Description

Serializes this element to JSON format and writes it to a file.

The SaveToJSONFile method converts the element tree structure to a JSON representation and saves it to the specified file path. The JSON output preserves the hierarchical structure, with element names as keys and values formatted appropriately for their types.

The aCompact parameter controls formatting: when True, the JSON is written on minimal lines with no extra whitespace; when False, the JSON is formatted with indentation for human readability.

JSON export is useful for debugging binary structures, creating human-editable versions of files, or transferring data between different tools and formats.

If the file cannot be written, an exception is raised.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileName | string | Full path where the JSON file should be saved |
| aCompact | Boolean | If True, output compact JSON; if False, output formatted JSON with indentation |

## Returns

This method does not return a value.

## Example

```pascal
var
    materialFile: TwbBGSMFile;
    binPath, jsonPath: string;
begin
    materialFile := TwbBGSMFile.Create;
    try
        binPath := 'C:\Games\Fallout4\Data\Materials\test.bgsm';
        jsonPath := 'C:\Temp\test_material.json';

        // Load binary and export to JSON
        materialFile.LoadFromFile(binPath);
        materialFile.SaveToJSONFile(jsonPath, False); // False = formatted output

        AddMessage('Exported to JSON: ' + jsonPath);
    finally
        materialFile.Free;
    end;
end;
```

## See Also

- [TdfElement.LoadFromJSONFile](TdfElement_LoadFromJSONFile.md)
- [TdfElement.SaveToFile](TdfElement_SaveToFile.md)
- [TdfElement.ToJSON](TdfElement_ToJSON.md)
- [TdfElement.FromJSON](TdfElement_FromJSON.md)
