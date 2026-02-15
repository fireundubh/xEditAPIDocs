# TdfElement.ToJSON

## Syntax

```pascal
function ToJSON(aCompact: Boolean): string;
```

## Description

Serializes this element to a JSON string representation.

The ToJSON method converts the element and its children into a JSON string. The JSON preserves the hierarchical structure with element names as keys and appropriately formatted values.

The aCompact parameter controls formatting: when True, the JSON is minimized with no extra whitespace; when False, the JSON includes indentation and line breaks for human readability.

This is useful for debugging, logging element state, or preparing data for export. The resulting JSON can be loaded back using FromJSON for round-trip serialization.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aCompact | Boolean | If True, output compact JSON; if False, output formatted JSON with indentation |

## Returns

Returns a JSON string representation of the element.

## Example

```pascal
var
    element: TdfElement;
    jsonCompact, jsonFormatted: string;
begin
    // Get compact JSON
    jsonCompact := element.ToJSON(True);
    AddMessage('Compact: ' + jsonCompact);

    // Get formatted JSON
    jsonFormatted := element.ToJSON(False);
    AddMessage('Formatted:');
    AddMessage(jsonFormatted);

    // Round-trip test
    element.FromJSON(jsonCompact);
end;
```

## See Also

- [TdfElement.FromJSON](TdfElement_FromJSON.md)
- [TdfElement.SaveToJSONFile](TdfElement_SaveToJSONFile.md)
- [TdfElement.LoadFromJSONFile](TdfElement_LoadFromJSONFile.md)
- [TdfElement.ToText](TdfElement_ToText.md)
