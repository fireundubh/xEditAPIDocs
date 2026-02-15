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
// Example 1: Update references after modifying record
begin
  if Assigned(e) then begin
    // Make changes to record
    SetElementEditValue(e, 'FULL', 'Modified Name');
    SetElementEditValue(e, 'DATA\Value', '500');

    // Update reference tracking
    UpdateRefs(e);
    AddMessage('Reference information updated');
  end;
end;

// Example 2: Refresh reference counts after adding/removing references
var
  beforeCount, afterCount: integer;
begin
  if Assigned(e) then begin
    beforeCount := ReferencedByCount(e);

    // External operation that might affect references
    // ... (e.g., another script adds FormID field pointing to this record)

    UpdateRefs(e);
    afterCount := ReferencedByCount(e);

    AddMessage(Format('Referenced by count changed from %d to %d',
      [beforeCount, afterCount]));
  end;
end;

// Example 3: Ensure references are tracked before iteration
var
  refRec: IwbMainRecord;
  i, count: integer;
begin
  if Assigned(e) then begin
    // Ensure reference information is current
    UpdateRefs(e);

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


