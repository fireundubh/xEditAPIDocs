# TdfElement.Def

## Syntax

```pascal
property Def: TdfDef;
```

## Description

Returns the definition object that defines the structure and behavior of this element.

The Def property provides access to the TdfDef object that serves as the template or schema for this element. The definition contains metadata such as the element's name, data type, default size, default value, and various callbacks that control element behavior. This relationship is analogous to the relationship between a class definition and an instance in object-oriented programming.

Every TdfElement is created from a TdfDef, and the definition remains constant throughout the element's lifetime.

This property is read-only.

## Parameters

This property has no parameters.

## Returns

Returns the TdfDef object that defines this element's structure.

## Example

```pascal
var
    element: TdfElement;
    def: TdfDef;
    defName: string;
begin
    def := element.Def;
    defName := def.Name;
    AddMessage('Element definition: ' + defName);
end;
```

## See Also

- [TdfDef.Name](TdfDef_Name.md)
- [TdfDef.DefaultDataSize](TdfDef_DefaultDataSize.md)
- [TdfElement.DataType](TdfElement_DataType.md)
- [TdfElement.Name](TdfElement_Name.md)
