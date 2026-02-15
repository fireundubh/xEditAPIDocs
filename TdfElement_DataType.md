# TdfElement.DataType

## Syntax

```pascal
property DataType: TdfDataType;
```

## Description

Returns the data type classification for this element as defined by its definition.

The DataType property indicates what kind of data this element represents in the binary format. The TdfDataType enumeration includes primitive types (dtU8, dtS8, dtU16, dtS16, dtU32, dtS32, dtU64, dtS64, dtFloat16, dtFloat32), raw data types (dtBytes, dtChars), and structural types (dtStruct, dtArray, dtUnion, dtMerge).

Understanding the data type is essential for proper interpretation and manipulation of binary file data. Use the constants dftNone, dftStruct, dftArray, dftUnion, dftMerge, dftBytes, dftChars, dftU8, dftS8, dftU16, dftS16, dftU32, dftS32, dftU64, dftS64, dftFloat16, dftFloat32 when comparing data types in scripts.

This property is read-only.

## Parameters

This property has no parameters.

## Returns

Returns the TdfDataType enumeration value indicating the element's data type.

## Example

```pascal
var
    element: TdfElement;
    dataType: Integer;
begin
    dataType := element.DataType;
    if dataType = dftStruct then
        AddMessage('Element is a structure')
    else if dataType = dftU32 then
        AddMessage('Element is a 32-bit unsigned integer');
end;
```

## See Also

- [TdfElement.Def](TdfElement_Def.md)
- [TdfElement.Name](TdfElement_Name.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.EditValue](TdfElement_EditValue.md)
