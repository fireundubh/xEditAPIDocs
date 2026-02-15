# TdfElement.Elements

## Syntax

```pascal
property Elements[const aPath: string]: TdfElement;
```

## Description

Returns the enabled child element at the specified path.

The Elements indexed property provides convenient path-based access to descendant elements. This is an alias for the EnabledElementByPath method and always searches only enabled elements.

The path uses backslash separators to navigate the hierarchy (e.g., "Header\Version" or "Blocks\[0]\Children"). Array elements are accessed using bracket notation with zero-based indices.

If the path does not resolve to an enabled element, returns nil.

This property is read-only.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aPath | string | The path to the child element using backslash separators |

## Returns

Returns the TdfElement at the specified path, or nil if not found or disabled.

## Example

```pascal
var
    nifFile: TdfElement;
    header, firstBlock: TdfElement;
begin
    // Access nested elements
    header := nifFile.Elements['Header'];
    if Assigned(header) then
        AddMessage('Header version: ' + header.Elements['Version'].EditValue);

    // Access array elements
    firstBlock := nifFile.Elements['Blocks\[0]'];
    if Assigned(firstBlock) then
        AddMessage('First block type: ' + firstBlock.Elements['Block Type'].EditValue);
end;
```

## See Also

- [TdfElement.ElementByPath](TdfElement_ElementByPath.md)
- [TdfElement.ElementByName](TdfElement_ElementByName.md)
- [TdfElement.Path](TdfElement_Path.md)
- [TdfElement.Items](TdfElement_Items.md)
