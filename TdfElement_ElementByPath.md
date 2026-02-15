# TdfElement.ElementByPath

## Syntax

```pascal
function ElementByPath(const aPath: string; aEnabledOnly: Boolean = True): TdfElement;
```

## Description

Navigates to and returns the descendant element at the specified path.

The ElementByPath method traverses the element hierarchy using a path string with backslash separators. It can navigate through multiple levels of the tree in a single call. Array elements are accessed using bracket notation with zero-based indices (e.g., "[0]", "[15]").

The aEnabledOnly parameter controls whether to navigate only through enabled elements (default) or include disabled ones. In most cases, you should use the default value of True.

If any part of the path cannot be resolved, returns nil. The path is case-sensitive for element names.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aPath | string | The path to navigate using backslash separators (e.g., "Header\Version" or "Blocks\[0]\Name") |
| aEnabledOnly | Boolean | If True (default), navigate only through enabled elements; if False, include disabled elements |

## Returns

Returns the TdfElement at the specified path, or nil if the path is invalid.

## Example

```pascal
var
    nifFile, version, firstBlock, translation: TdfElement;
begin
    // Navigate to nested elements
    version := nifFile.ElementByPath('Header\Version');
    if Assigned(version) then
        AddMessage('NIF Version: ' + version.EditValue);

    // Navigate through arrays
    firstBlock := nifFile.ElementByPath('Blocks\[0]');
    if Assigned(firstBlock) then
        AddMessage('First block type: ' + firstBlock.ElementByName('Block Type').EditValue);

    // Deep navigation
    translation := nifFile.ElementByPath('Blocks\[0]\Translation\X');
    if Assigned(translation) then
        translation.NativeValue := 100.0;
end;
```

## See Also

- [TdfElement.ElementByName](TdfElement_ElementByName.md)
- [TdfElement.Elements](TdfElement_Elements.md)
- [TdfElement.Path](TdfElement_Path.md)
- [TdfElement.NativeValues](TdfElement_NativeValues.md)
