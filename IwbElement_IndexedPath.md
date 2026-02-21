# IndexedPath

## Syntax

```pascal
function IndexedPath(AElement: IwbElement; AFromFile: Boolean): String;
```

## Description

Returns a compact, navigable path for an element using signatures and names instead of verbose display names. Each path segment uses the element's 4-character signature when available (e.g., `FULL`, `ACBS`, `CTDA`), the element's name for struct fields without signatures (e.g., `Weight`, `Value`), or a zero-based index in brackets for array elements (e.g., `[0]`, `[3]`).

If `AFromFile` is true, the path starts from the file level. If false, the path starts from the main record's children, excluding file and group record prefixes.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the path from |
| AFromFile | Boolean | Whether to include the file-level prefix in the path |

## Returns

Returns the path as a string using signatures, names, and array indices.

## Example

```pascal
// Example 1: Get named path for a simple sub-record
var
  element: IwbElement;
begin
  if Assigned(e) then begin
    element := ElementBySignature(e, 'FULL');
    if Assigned(element) then begin
      AddMessage(IndexedPath(element, False));
      // Output: "FULL"
    end;
  end;
end;

// Example 2: Get named path for a nested element
var
  element: IwbElement;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA\Weight');
    if Assigned(element) then begin
      AddMessage(IndexedPath(element, False));
      // Output: "DATA\Weight"
    end;
  end;
end;

// Example 3: Get named path for an array element's child
var
  element: IwbElement;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'Conditions\[0]\CTDA\Type');
    if Assigned(element) then begin
      AddMessage(IndexedPath(element, True));
      // Output: "TestPlugin.esp\WEAP\Conditions\[0]\CTDA\Type"
      AddMessage(IndexedPath(element, False));
      // Output: "Conditions\[0]\CTDA\Type"
    end;
  end;
end;

// Example 4: Log paths of all direct children
var
  container: IwbContainer;
  child: IwbElement;
  i: integer;
begin
  if Assigned(e) and Supports(e, IwbContainer, container) then
    for i := 0 to Pred(ElementCount(container)) do begin
      child := ElementByIndex(container, i);
      if Assigned(child) then
        AddMessage(Format('[%d] %s', [i, IndexedPath(child, False)]));
    end;
end;
```

## See Also

- [Path](IwbElement_Path.md)
- [FullPath](IwbElement_FullPath.md)
- [PathName](IwbElement_PathName.md)
- [Name](IwbElement_Name.md)
- [SortOrderOf](IwbElement_SortOrderOf.md)
