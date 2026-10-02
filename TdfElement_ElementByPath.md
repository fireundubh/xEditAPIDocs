# TdfElement.ElementByPath

## Syntax

```pascal
function ElementByPath(const aPath: string; aEnabledOnly: Boolean): TdfElement;
```

Access via: `element.ElementByPath(Path, EnabledOnly)`

## Description

Navigates to and returns the descendant element at the specified path.

The ElementByPath method traverses the element hierarchy using a path string with backslash separators. It can navigate through multiple levels of the tree in a single call. Array elements are accessed using bracket notation with zero-based indices (e.g., "[0]", "[15]").

Both arguments are required. aEnabledOnly is not optional: pass True to follow only enabled elements, or False to include disabled elements.

If any part of the path cannot be resolved, returns nil. The path is case-sensitive for element names.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aPath | string | The path to navigate using backslash separators (e.g., "Header\Version" or "Blocks\[0]\Name") |
| aEnabledOnly | Boolean | Required. If True, navigate only through enabled elements; if False, include disabled elements |

## Returns

Returns the TdfElement at the specified path, or nil if the path is invalid.

## Example

```pascal
var
    nifFile, version, firstBlock, blockType, translation: TdfElement;
begin
    version := nifFile.ElementByPath('Header\Version', True);
    if Assigned(version) then
        AddMessage('NIF Version: ' + version.EditValue);

    firstBlock := nifFile.ElementByPath('Blocks\[0]', True);
    if Assigned(firstBlock) then begin
        blockType := firstBlock.ElementByName('Block Type', True);
        if Assigned(blockType) then
            AddMessage('First block type: ' + blockType.EditValue);
    end;

    translation := nifFile.ElementByPath('Blocks\[0]\Translation\X', True);
    if Assigned(translation) then
        translation.NativeValue := 100.0;
end;
```

## See Also

- [TdfElement.ElementByName](TdfElement_ElementByName.md)
- [TdfElement.Elements](TdfElement_Elements.md)
- [TdfElement.Path](TdfElement_Path.md)
- [TdfElement.NativeValues](TdfElement_NativeValues.md)
