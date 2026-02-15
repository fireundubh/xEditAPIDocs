# ElementAssign

## Syntax

```pascal
function ElementAssign(AContainer: IwbContainer; AIndex: integer; ASource: IwbElement; AOnlySK: boolean): IwbElement;
```

## Description

Copies or creates elements within a container element.

Returns the newly created or copied element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The destination container element |
| AIndex | integer | The position index where to place the new element (use HighInteger to append, LowInteger or negative for non-arrays) |
| ASource | IwbElement | The source element to copy from (can be nil to create blank element) |
| AOnlySK | boolean | Sorted Key Only flag (use false for normal operations) |

## Returns

Returns the newly created or copied element as an IwbElement interface.

## Example

```pascal
// Example 1: Copy element from one record to another
var
  destRec: IwbMainRecord;
  sourceElement, newElement: IwbElement;
  destContainer: IwbContainer;
begin
  destRec := RecordByFormID(FileByIndex(0), $00012345, True);
  if Assigned(e) and Assigned(destRec) then begin
    sourceElement := ElementByPath(e, 'KWDA');
    if Assigned(sourceElement) then begin
      destContainer := destRec;
      newElement := ElementAssign(destContainer, HighInteger, sourceElement, False);
      if Assigned(newElement) then
        AddMessage(Format('Copied KWDA to %s', [EditorID(destRec)]));
    end;
  end;
end;

// Example 2: Duplicate array element within same container
var
  keywords: IwbContainer;
  sourceElement, copiedElement: IwbElement;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) > 0) then begin
      sourceElement := ElementByIndex(keywords, 0);
      if Assigned(sourceElement) then begin
        // Append copy at end
        copiedElement := ElementAssign(keywords, HighInteger, sourceElement, False);
        if Assigned(copiedElement) then
          AddMessage(Format('Duplicated keyword in %s', [EditorID(e)]));
      end;
    end;
  end;
end;

// Example 3: Create blank element and populate
var
  conditions: IwbContainer;
  newCondition, funcElement: IwbElement;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      // Create blank element (nil source)
      newCondition := ElementAssign(conditions, HighInteger, nil, False);
      if Assigned(newCondition) then begin
        SetToDefault(newCondition);
        funcElement := ElementByPath(newCondition, 'CTDA\Function');
        if Assigned(funcElement) then begin
          SetEditValue(funcElement, 'GetItemCount');
          AddMessage(Format('Added new condition to %s', [EditorID(e)]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [IsEditable](IwbElement_IsEditable.md)


