# CopyByPath

## Syntax

```pascal
function CopyByPath(AContainer: IwbContainer; APath: string; ASource: IwbElement): IwbElement;
```

## Description

Copies a source element into a container at the slot identified by a path or signature string. This is a convenience wrapper around ElementAssign that resolves the path to the correct sort order index automatically, eliminating the need to manually determine numeric index values.

The function first tries to find the target element by path. If not found and the path is exactly 4 characters, it tries to find it by signature. If the target element is found, the source is assigned at the target's sort order. If no target is found, the source is appended using HighInteger (useful for arrays).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The destination container (typically a main record) |
| APath | string | The path or signature identifying the target element slot (e.g., 'FULL', 'EDID', 'DATA\Weight') |
| ASource | IwbElement | The source element to copy from |

## Returns

Returns the newly created or copied element as an IwbElement interface.

## Example

```pascal
// Example 1: Copy FULL name from one record to another
var
  sourceRec, destRec: IwbMainRecord;
  sourceName: IwbElement;
begin
  sourceRec := RecordByFormID(FileByIndex(0), $00012345, True);
  destRec := RecordByFormID(FileByIndex(0), $00067890, True);
  if Assigned(sourceRec) and Assigned(destRec) then begin
    sourceName := ElementBySignature(sourceRec, 'FULL');
    if Assigned(sourceName) then begin
      CopyByPath(destRec, 'FULL', sourceName);
      AddMessage('Copied FULL name to destination record');
    end;
  end;
end;

// Example 2: Copy a nested struct element by path
var
  sourceRec, destRec: IwbMainRecord;
  sourceData: IwbElement;
begin
  sourceRec := RecordByFormID(FileByIndex(0), $00012345, True);
  destRec := RecordByFormID(FileByIndex(0), $00067890, True);
  if Assigned(sourceRec) and Assigned(destRec) then begin
    sourceData := ElementByPath(sourceRec, 'ACBS');
    if Assigned(sourceData) then begin
      CopyByPath(destRec, 'ACBS', sourceData);
      AddMessage('Copied ACBS configuration');
    end;
  end;
end;

// Example 3: Copy multiple sub-elements between records
var
  sourceRec, destRec: IwbMainRecord;
  signatures: array[0..2] of string;
  i: integer;
  sourceElem: IwbElement;
begin
  sourceRec := RecordByFormID(FileByIndex(0), $00012345, True);
  destRec := RecordByFormID(FileByIndex(0), $00067890, True);
  signatures[0] := 'FULL';
  signatures[1] := 'EDID';
  signatures[2] := 'ACBS';
  if Assigned(sourceRec) and Assigned(destRec) then
    for i := 0 to 2 do begin
      sourceElem := ElementBySignature(sourceRec, signatures[i]);
      if Assigned(sourceElem) then
        CopyByPath(destRec, signatures[i], sourceElem);
    end;
end;
```

## See Also

- [ElementAssign](IwbElement_ElementAssign.md)
- [Add](IwbContainer_Add.md)
- [SortOrderOf](IwbElement_SortOrderOf.md)
- [ElementByPath](IwbContainer_ElementByPath.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)

