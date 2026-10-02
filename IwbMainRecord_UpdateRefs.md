# UpdateRefs

## Syntax

```pascal
procedure UpdateRefs(ARecord: IwbMainRecord);
```

## Description

Rebuilds outgoing references for `ARecord` when reference building is already active for that record.

If references have never been built, this call does nothing. Use [BuildRef](IwbElement_BuildRef.md) to build them. If the lists are already current, the rebuild is skipped. This refreshes records this record points at. It does not rescan the load order for records that point at `ARecord`. Only a main record can be passed.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to update reference information for |

## Returns

Returns nothing.

## Example

```pascal
// Example 1: Refresh outgoing references after they have been built
begin
  if Assigned(e) then begin
    BuildRef(e);
    UpdateRefs(e);
    AddMessage(Format('Outgoing references: %d', [ReferencesCount(e)]));
  end;
end;

// Example 2: UpdateRefs does nothing until references have been built
var
  beforeCount, afterCount: integer;
begin
  if Assigned(e) then begin
    beforeCount := ReferencesCount(e);
    UpdateRefs(e);
    afterCount := ReferencesCount(e);
    AddMessage(Format('Before BuildRef: %d, after UpdateRefs: %d', [beforeCount, afterCount]));

    BuildRef(e);
    AddMessage(Format('After BuildRef: %d', [ReferencesCount(e)]));
  end;
end;

// Example 3: Build references before iteration
var
  refRec: IwbMainRecord;
  i, count: integer;
begin
  if Assigned(e) then begin
    BuildRef(e);

    count := ReferencesCount(e);
    AddMessage(Format('Processing %d outgoing references...', [count]));

    for i := 0 to count - 1 do begin
      refRec := ReferencesByIndex(e, i);
      if Assigned(refRec) then
        AddMessage(Format('  %s', [EditorID(refRec)]));
    end;
  end;
end;
```

## See Also

- [BuildRef](IwbElement_BuildRef.md)
- [ReferencesCount](IwbMainRecord_ReferencesCount.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)


