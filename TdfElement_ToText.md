# TdfElement.ToText

## Syntax

```pascal
function ToText: string;
```

Access via: `element.ToText`

## Description

Converts this element and its children to a human-readable text representation.

The ToText method generates a formatted text dump of the element structure, showing the hierarchy, element names, and values. This is primarily used for debugging and logging purposes to quickly inspect the contents of a binary file structure.

The output format is indented with tabs to show the tree structure. Value elements append their EditValue. A disabled element returns an empty string and is omitted. The script method takes no arguments.

This differs from ToJSON in that it produces a more informal, human-oriented output rather than a structured data format.

## Parameters

This method has no parameters.

## Returns

Returns a formatted text representation of the element as a string.

## Example

```pascal
var
    nifFile: TwbNifFile;
    header: TdfElement;
    textDump: string;
begin
    nifFile := TwbNifFile.Create;
    try
        nifFile.LoadFromFile('test.nif');
        textDump := nifFile.ToText;
        AddMessage(textDump);

        header := nifFile.Elements['Header'];
        if Assigned(header) then begin
            textDump := header.ToText;
            AddMessage('Header:');
            AddMessage(textDump);
        end;
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
