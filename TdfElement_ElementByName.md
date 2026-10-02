# TdfElement.ElementByName

## Syntax

```pascal
function ElementByName(const aName: string; aEnabledOnly: Boolean): TdfElement;
```

Access via: `element.ElementByName(Name, EnabledOnly)`

## Description

Searches for and returns the first direct child element with the specified name.

The ElementByName method performs a case-sensitive search through this element's immediate children for an element whose Name property matches the specified string. It does not search recursively through descendants.

Both arguments are required. aEnabledOnly is not optional: pass True to search only enabled elements, or False to include disabled elements.

If no matching element is found, returns nil.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aName | string | The name of the child element to search for (case-sensitive) |
| aEnabledOnly | Boolean | Required. If True, search only enabled elements; if False, search all elements |

## Returns

Returns the first matching TdfElement, or nil if not found.

## Example

```pascal
var
    nifBlock, translation, childX, children: TdfElement;
begin
    translation := nifBlock.ElementByName('Translation', True);
    if Assigned(translation) then begin
        childX := translation.Elements['X'];
        if Assigned(childX) then
            AddMessage('Translation X: ' + childX.EditValue);
    end;

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
