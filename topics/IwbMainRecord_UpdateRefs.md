# UpdateRefs

## Syntax

```pascal
procedure UpdateRefs(ARecord: IwbMainRecord);
```

## Description

Updates reference information for `ARecord`, if reference information is not already updating

If reference information is already updating, the procedure will abort.

Unlike [BuildRef](IwbElement_BuildRef.md), only an `IwbMainRecord` can be passed as an argument to this function.

## Example

```pascal
UpdateRefs(e);  // `e` must be an IwbMainRecord, unlike BuildRef
```

## See Also

- [BuildRef](IwbElement_BuildRef.md)


