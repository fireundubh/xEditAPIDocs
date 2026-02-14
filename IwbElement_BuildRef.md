# BuildRef

## Syntax

```pascal
procedure BuildRef(AElement: IwbElement);
```

## Description

Rebuilds the FormID reference tracking information for the element and its descendants.

This function calls the element's BuildRef method, which scans the element tree for FormID fields and updates the internal reference tracking (used by ReferencedBy/ReferencesBy). Accepts any element type (files, records, containers, subrecords). Essential for populating reference counts before using ReferencedByCount or similar functions. May be slow for large files or heavily-referenced records. Some optimizations skip processing if references are already current or the file is a delta patch.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element for which to rebuild reference information |

## Example

```pascal
var
    f: IwbFile
begin
    f := GetFile(e);
    BuildRef(f);
end;
```

## See Also

- [LinksTo](IwbElement_LinksTo.md)
- [CanContainFormIDs](IwbElement_CanContainFormIDs.md)
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [UpdateRefs](IwbMainRecord_UpdateRefs.md)


