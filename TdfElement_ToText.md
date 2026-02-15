# TdfElement.ToText

## Syntax

```pascal
function ToText: string;
```

## Description

Converts this element and its children to a human-readable text representation.

The ToText method generates a formatted text dump of the element structure, showing the hierarchy, element names, and values. This is primarily used for debugging and logging purposes to quickly inspect the contents of a binary file structure.

The output format is indented to show the tree structure, with each level indented further than its parent. Values are shown in their EditValue representation. The exact format may vary based on element type and definition.

This differs from ToJSON in that it produces a more informal, human-oriented output rather than a structured data format.

## Parameters

This method has no parameters.

## Returns

Returns a formatted text representation of the element as a string.

## Example

```pascal
var
    nifFile: TwbNifFile;
    textDump: string;
begin
    nifFile := TwbNifFile.Create;
    try
        nifFile.LoadFromFile('test.nif');

        // Get text representation
        textDump := nifFile.ToText;
        AddMessage(textDump);

        // Or dump specific elements
        textDump := nifFile.Elements['Header'].ToText;
        AddMessage('Header:');
        AddMessage(textDump);
    finally
        nifFile.Free;
    end;
end;
```

## See Also

- [TdfElement.ToJSON](TdfElement_ToJSON.md)
- [TdfElement.EditValue](TdfElement_EditValue.md)
- [TdfElement.Path](TdfElement_Path.md)
- [TdfElement.Name](TdfElement_Name.md)
