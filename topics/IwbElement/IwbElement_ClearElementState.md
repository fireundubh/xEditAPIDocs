# ClearElementState

## Syntax

```pascal
procedure ClearElementState(AElement: IwbElement; AState: TwbElementState);
```

## Description

Manipulates the internal flags of an element.

This procedure allows you to clear specific state flags on elements. Common usage includes clearing the modified state of elements.

## Element States

- `esModified`
- `esInternalModified`
- `esUnsaved`
- `esSortKeyValid`
- `esExtendedSortKeyValid`
- `esHidden`
- `esParentHidden`
- `esParentHiddenChecked`
- `esNotReachable`
- `esReachable`
- `esTagged`
- `esDeciding`
- `esResolving`
- `esNotSuitableToAddTo`

## Example

```pascal
var
    element: IwbElement;
begin
    ClearElementState(element, esModified);
end;
```

## See Also

- [GetElementState](IwbElement_GetElementState.md)
- [SetElementState](IwbElement_SetElementState.md)
