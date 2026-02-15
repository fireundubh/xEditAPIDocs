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
// Example 1: Build references for entire file
var
  pluginFile: IwbFile;
begin
  if Assigned(e) then begin
    pluginFile := GetFile(e);
    if Assigned(pluginFile) then begin
      AddMessage('Building references for ' + GetFileName(pluginFile));
      BuildRef(pluginFile);
      AddMessage('Reference building complete');
    end;
  end;
end;

// Example 2: Build references for specific record before checking
var
  refCount: integer;
begin
  if Assigned(e) then begin
    BuildRef(e);
    refCount := ReferencedByCount(e);
    AddMessage(Format('%s is referenced by %d records',
      [EditorID(e), refCount]));
  end;
end;

// Example 3: Build references for container and analyze
var
  keywords: IwbContainer;
  i: integer;
  kwdElement: IwbElement;
  kwdRecord: IwbMainRecord;
  kwdRefCount: integer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      BuildRef(keywords);
      AddMessage('Keyword reference counts:');
      for i := 0 to ElementCount(keywords) - 1 do begin
        kwdElement := ElementByIndex(keywords, i);
        if Assigned(kwdElement) then begin
          kwdRecord := LinksTo(kwdElement);
          if Assigned(kwdRecord) then begin
            kwdRefCount := ReferencedByCount(kwdRecord);
            AddMessage(Format('  %s: %d references',
              [EditorID(kwdRecord), kwdRefCount]));
          end;
        end;
      end;
    end;
  end;
end;
```

## See Also

- [LinksTo](IwbElement_LinksTo.md)
- [CanContainFormIDs](IwbElement_CanContainFormIDs.md)
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [UpdateRefs](IwbMainRecord_UpdateRefs.md)


