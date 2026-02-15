# TdfElement.Move

## Syntax

```pascal
procedure Move(CurIndex, NewIndex: Integer);
```

## Description

Moves a child element from one position to another within this container.

The Move method relocates a child element from CurIndex to NewIndex, shifting other elements as necessary. This is useful for reordering array elements without the overhead of removing and re-adding them.

Both indices must be valid (0 to Count-1), or an exception will be raised. If CurIndex equals NewIndex, the method does nothing.

For structure elements, Move may raise an exception as structures typically maintain a fixed field order defined by their definition. Use this method primarily with array elements.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| CurIndex | Integer | Zero-based index of the element to move |
| NewIndex | Integer | Zero-based index of the destination position |

## Returns

This method does not return a value.

## Example

```pascal
var
    arrayElement: TdfElement;
begin
    // Move element from index 2 to index 0 (move to front)
    arrayElement.Move(2, 0);

    // Move element from index 0 to end
    arrayElement.Move(0, arrayElement.Count - 1);

    // Swap adjacent elements
    arrayElement.Move(5, 6);
end;
```

## See Also

- [TdfElement.Delete](TdfElement_Delete.md)
- [TdfElement.Add](TdfElement_Add.md)
- [TdfElement.Index](TdfElement_Index.md)
- [TdfElement.IndexOf](TdfElement_IndexOf.md)
