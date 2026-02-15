# TdfDef.Name

## Syntax

```pascal
property Name: string;
```

## Description

Returns the definition's name identifier as specified when the definition was created.

The Name property holds the string identifier assigned to this data format definition. This is typically a descriptive name that identifies what this definition represents in a binary file structure (e.g., "NiNode", "BSLightingShaderProperty", "Version"). The name is used for lookup operations and structural documentation of binary formats.

This property is read-only and is set during the definition's construction.

## Parameters

This property has no parameters.

## Returns

Returns the name of the definition as a string.

## Example

```pascal
var
    def: TdfDef;
    defName: string;
begin
    defName := def.Name;
    AddMessage('Definition name: ' + defName);
end;
```

## See Also

- [TdfDef.DefaultDataSize](TdfDef_DefaultDataSize.md)
- [TdfDef.Size](TdfDef_Size.md)
- [TdfElement.Name](TdfElement_Name.md)
- [TdfElement.Def](TdfElement_Def.md)
