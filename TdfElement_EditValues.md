# TdfElement.EditValues

## Syntax

```pascal
property EditValues[const aPath: string]: string;
```

## Description

Gets or sets the edit value (human-readable string) of a child element specified by path.

The EditValues indexed property provides convenient access to descendant elements' string representations without explicitly navigating the tree. The path parameter uses backslash separators to traverse the hierarchy (e.g., "Material Name" or "Properties\[0]\Type").

This is equivalent to calling ElementByPath followed by accessing EditValue, but more concise. The path navigation respects the Enabled property - only enabled elements are accessible by default.

If the path does not resolve to a valid element, reading returns an empty string and writing has no effect.

This property is read-write.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aPath | string | The path to the child element using backslash separators |

## Returns

Returns the edit value of the element at the specified path as a string, or empty string if the path is invalid.

## Example

```pascal
var
    nifFile: TdfElement;
    version, nodeName: string;
begin
    // Read values using path
    version := nifFile.EditValues['Header\Version'];
    nodeName := nifFile.EditValues['Blocks\[0]\Name'];
    AddMessage('Version: ' + version + ', Node: ' + nodeName);

    // Set values using path
    nifFile.EditValues['Header\Creator'] := 'xEdit Script';
    nifFile.EditValues['Blocks\[1]\Alpha'] := '128';
end;
```

## See Also

- [TdfElement.NativeValues](TdfElement_NativeValues.md)
- [TdfElement.EditValue](TdfElement_EditValue.md)
- [TdfElement.ElementByPath](TdfElement_ElementByPath.md)
- [TdfElement.Path](TdfElement_Path.md)
