# TdfElement.Name

## Syntax

```pascal
property Name: string;
```

## Description

Returns the element's name as defined by its definition.

The Name property retrieves the identifier for this element from its TdfDef. For elements in binary file structures like NIF files, this typically corresponds to field names defined in the format specification (e.g., "Num Vertices", "Translation", "Material Name"). For array elements, the name usually includes an index.

This property is read-only and is inherited from the element's definition.

## Parameters

This property has no parameters.

## Returns

Returns the name of the element as a string.

## Example

```pascal
var
    element: TdfElement;
    elemName: string;
begin
    elemName := element.Name;
    AddMessage('Element name: ' + elemName);
end;
```

## See Also

- [TdfElement.Path](TdfElement_Path.md)
- [TdfElement.Def](TdfElement_Def.md)
- [TdfDef.Name](TdfDef_Name.md)
- [TdfElement.ElementByName](TdfElement_ElementByName.md)
