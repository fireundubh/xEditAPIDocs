# TdfElement.FromJSON

## Syntax

```pascal
procedure FromJSON(const aText: string);
```

## Description

Deserializes JSON text and populates this element with the parsed data.

The FromJSON method parses a JSON string and loads the data into this element. The JSON structure must be compatible with the element's definition - field names should match element names, and the hierarchy should align with the element structure.

This is useful for programmatically loading element data from JSON strings, whether from configuration files, network responses, or generated content. It complements ToJSON for round-trip serialization.

Any existing data in the element is replaced with the newly parsed data.

If the JSON is malformed or incompatible with the element structure, an exception may be raised.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aText | string | The JSON string to parse and load |

## Returns

This method does not return a value.

## Example

```pascal
var
    element: TdfElement;
    jsonText: string;
begin
    jsonText := '{"X": 100.0, "Y": 200.0, "Z": 50.0}';

    // Load from JSON string
    element.FromJSON(jsonText);

    // Access loaded data
    AddMessage('X: ' + element.Elements['X'].EditValue);
    AddMessage('Y: ' + element.Elements['Y'].EditValue);
    AddMessage('Z: ' + element.Elements['Z'].EditValue);
end;
```

## See Also

- [TdfElement.ToJSON](TdfElement_ToJSON.md)
- [TdfElement.LoadFromJSONFile](TdfElement_LoadFromJSONFile.md)
- [TdfElement.SaveToJSONFile](TdfElement_SaveToJSONFile.md)
- [TdfElement.Assign](TdfElement_Assign.md)
