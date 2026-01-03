# BuildRef

## Syntax

```pascal
procedure BuildRef(AElement: IwbElement);
```

## Description

Updates the reference information for `AElement`, regardless of whether references are updating

Unlike `UpdateRefs`, this function will accept any of these argument types:

- `IwbContainer`
- `IwbFile`
- `IwbGroupRecord`
- `IwbMainRecord`
- `IwbSubRecord`
- `TwbValueBase`

If references are updating for an `IwbFile` and references are not out-of-date, or if the plugin is a delta patch, the procedure will abort.

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

- [UpdateRefs](IwbMainRecord_UpdateRefs.md)


