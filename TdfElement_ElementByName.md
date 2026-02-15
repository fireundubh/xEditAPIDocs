# TdfElement.ElementByName

## Syntax

```pascal
function ElementByName(const aName: string; aEnabledOnly: Boolean = True): TdfElement;
```

## Description

Searches for and returns the first direct child element with the specified name.

The ElementByName method performs a case-sensitive search through this element's immediate children for an element whose Name property matches the specified string. It does not search recursively through descendants.

The aEnabledOnly parameter controls whether to search only enabled elements (default) or all elements including disabled ones. In most cases, you should use the default value of True to respect element visibility.

If no matching element is found, returns nil.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aName | string | The name of the child element to search for (case-sensitive) |
| aEnabledOnly | Boolean | If True (default), search only enabled elements; if False, search all elements |

## Returns

Returns the first matching TdfElement, or nil if not found.

## Example

```pascal
var
    nifBlock, translation, children: TdfElement;
begin
    // Find child by name (enabled only)
    translation := nifBlock.ElementByName('Translation');
    if Assigned(translation) then
        AddMessage('Translation X: ' + translation.Elements['X'].EditValue);

    // Find child including disabled elements
    children := nifBlock.ElementByName('Children', False);
    if Assigned(children) then
        AddMessage('Children array found (Count: ' + IntToStr(children.Count) + ')');
end;
```

## See Also

- [TdfElement.ElementByPath](TdfElement_ElementByPath.md)
- [TdfElement.Elements](TdfElement_Elements.md)
- [TdfElement.Name](TdfElement_Name.md)
- [TdfElement.Enabled](TdfElement_Enabled.md)
