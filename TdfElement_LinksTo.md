# TdfElement.LinksTo

## Syntax

```pascal
function LinksTo: TdfElement;
```

## Description

Returns the element that this element links to, if it represents a reference or pointer.

The LinksTo method is primarily used with NIF reference types (like TwbNiRef) that contain indices or pointers to other elements in the structure. For example, in NIF files, many fields contain block indices that reference other blocks in the file.

If the element definition has an OnLinksTo callback defined, that callback determines what element is returned. For non-reference elements or invalid references, this returns nil.

This is analogous to the LinksTo functionality in xEdit's plugin editor, where references can be resolved to their target records.

## Parameters

This method has no parameters.

## Returns

Returns the TdfElement that this element references, or nil if not applicable or invalid.

## Example

```pascal
var
    refElement, targetElement: TdfElement;
begin
    // Resolve a reference
    targetElement := refElement.LinksTo;
    if Assigned(targetElement) then begin
        AddMessage('Reference points to: ' + targetElement.Name);
        AddMessage('Target path: ' + targetElement.Path);
    end else
        AddMessage('Reference is nil or invalid');
end;
```

## See Also

- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.ElementByPath](TdfElement_ElementByPath.md)
- [TdfElement.Root](TdfElement_Root.md)
