# LinksTo

## Syntax

```pascal
function LinksTo(AElement: IwbElement): IwbElement;
```

## Description

Resolves and returns the element or record that this element references.

This function retrieves the LinksTo property, which resolves FormID references to their target records or elements. For FormID fields, it returns the IwbMainRecord being referenced. For other reference types, it may return the appropriate target element. Returns nil (unassigned) if the element is not a reference type, the reference is invalid, or the target cannot be found.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the linked reference from |

## Returns

Returns the referenced element as an IwbElement interface, or nil if no reference exists.

## Example

```pascal
// Example 1: Follow FormID reference to target record
var
  baseElement: IwbElement;
  baseRecord: IwbMainRecord;
  baseEdid: string;
begin
  if Assigned(e) then begin
    baseElement := ElementByPath(e, 'NAME');
    if Assigned(baseElement) then begin
      baseRecord := LinksTo(baseElement);
      if Assigned(baseRecord) then begin
        baseEdid := EditorID(baseRecord);
        AddMessage(Format('%s references base object: %s', [EditorID(e), baseEdid]));
      end;
    end;
  end;
end;

// Example 2: Traverse keyword array references
var
  keywords: IwbContainer;
  i: integer;
  kwdaElement: IwbElement;
  kwdaRecord: IwbMainRecord;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      AddMessage('Keywords for ' + EditorID(e) + ':');
      for i := 0 to ElementCount(keywords) - 1 do begin
        kwdaElement := ElementByIndex(keywords, i);
        if Assigned(kwdaElement) then begin
          kwdaRecord := LinksTo(kwdaElement);
          if Assigned(kwdaRecord) then
            AddMessage('  [' + IntToStr(i) + '] ' + EditorID(kwdaRecord));
        end;
      end;
    end;
  end;
end;

// Example 3: Check ingredient effects from alchemy recipe
var
  effects: IwbContainer;
  i: integer;
  effectElement, baseElement: IwbElement;
  effectRecord: IwbMainRecord;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      for i := 0 to ElementCount(effects) - 1 do begin
        effectElement := ElementByIndex(effects, i);
        if Assigned(effectElement) then begin
          baseElement := ElementByPath(effectElement, 'EFID');
          if Assigned(baseElement) then begin
            effectRecord := LinksTo(baseElement);
            if Assigned(effectRecord) then
              AddMessage(Format('Effect %d: %s', [i, EditorID(effectRecord)]));
          end;
        end;
      end;
    end;
  end;
end;
```

## See Also

- [CanContainFormIDs](IwbElement_CanContainFormIDs.md)
- [BuildRef](IwbElement_BuildRef.md)
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)


