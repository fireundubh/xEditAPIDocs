# UpdateRefs

## Syntax

```pascal
procedure UpdateRefs(ARecord: IwbMainRecord);
```

## Description

Updates reference information for `ARecord`, if reference information is not already updating

If reference information is already updating, the procedure will abort.

Unlike [BuildRef](IwbElement_BuildRef.md), only an `IwbMainRecord` can be passed as an argument to this function.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to update reference information for |

## Example

```pascal
UpdateRefs(e);  // `e` must be an IwbMainRecord, unlike BuildRef
```

## See Also

- [BuildRef](IwbElement_BuildRef.md)
- [ReferencesCount](IwbMainRecord_ReferencesCount.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)


