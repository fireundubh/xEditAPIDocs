# TdfElement.NativeValues

## Syntax

```pascal
property NativeValues[const aPath: string]: Variant;
```

## Description

Gets or sets the native value of a child element specified by path.

The NativeValues indexed property provides convenient access to descendant elements without explicitly navigating the tree. The path parameter uses backslash separators to traverse the hierarchy (e.g., "Translation\X" or "Children\[0]\Name").

This is equivalent to calling ElementByPath followed by accessing NativeValue, but in a single call. You cannot chain these operations (e.g., `element.ElementByPath('Name').NativeValue`) because the scripting engine cannot resolve property access on the Variant returned by ElementByPath. Use NativeValues whenever you need to read or write a child element's native value by path.

If you already have a reference to the specific element, use NativeValue directly instead.

If the path does not resolve to a valid element, reading returns Null and writing has no effect.

This property is read-write.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aPath | string | The path to the child element using backslash separators |

## Returns

Returns the native value of the element at the specified path as a Variant, or Null if the path is invalid.

## Example

```pascal
var
    nifBlock: TdfElement;
    xValue, yValue: Double;
begin
    // Read values using path
    xValue := nifBlock.NativeValues['Translation\X'];
    yValue := nifBlock.NativeValues['Translation\Y'];
    AddMessage('Position: ' + FloatToStr(xValue) + ', ' + FloatToStr(yValue));

    // Set values using path
    nifBlock.NativeValues['Translation\Z'] := 100.0;
    nifBlock.NativeValues['Children\[0]\Flags'] := 14;
end;
```

## See Also

- [TdfElement.EditValues](TdfElement_EditValues.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.ElementByPath](TdfElement_ElementByPath.md)
- [TdfElement.Path](TdfElement_Path.md)
