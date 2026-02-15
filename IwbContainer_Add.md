# Add

## Syntax

```pascal
function Add(AContainer: IwbContainer; ANameOrSignature: string; ASilent: boolean): IwbElement;
```

## Description

Creates and adds a new child element to the container by name or signature.

This function calls the container's Add method, which creates a new element based on the provided name or signature string and appends it to the container. The ASilent parameter controls whether change notifications are suppressed. Returns the newly created IwbElement. The element type created depends on the container's definition and the provided name/signature. Commonly used for adding new array elements or optional fields.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to add the element to |
| ANameOrSignature | string | The name or signature of the element to add |
| ASilent | boolean | If true, suppresses notifications during the operation |

## Returns

Returns the newly created element as an IwbElement interface.

## Example

```pascal
// Example 1: Add element to array
var
  keywords: IwbContainer;
  newKeyword: IwbElement;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      newKeyword := Add(keywords, 'Keyword', true);
      if Assigned(newKeyword) then begin
        SetEditValue(newKeyword, '00012345');
        AddMessage('Added keyword');
      end;
    end;
  end;
end;

// Example 2: Add multiple array elements
var
  conditions: IwbContainer;
  condition: IwbElement;
  i: integer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      BeginUpdate(conditions);
      try
        for i := 0 to 2 do begin
          condition := Add(conditions, 'Condition', true);
          if Assigned(condition) then begin
            SetElementEditValue(condition, 'CTDA\Type', '10000000');
            SetElementEditValue(condition, 'CTDA\Comparison Value', IntToStr(i));
            AddMessage(Format('Added condition %d', [i]));
          end;
        end;
      finally
        EndUpdate(conditions);
      end;
    end;
  end;
end;

// Example 3: Add optional struct element
var
  effects: IwbContainer;
  effect: IwbElement;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      effect := Add(effects, 'Effect', false); // Not silent - trigger notifications
      if Assigned(effect) then begin
        SetElementEditValue(effect, 'EFID', 'RestoreHealth');
        SetElementEditValue(effect, 'EFIT\Magnitude', '25');
        SetElementEditValue(effect, 'EFIT\Duration', '0');
        AddMessage('Added restore health effect');
      end;
    end;
  end;
end;
```

## See Also

- [AddElement](IwbContainer_AddElement.md)
- [InsertElement](IwbContainer_InsertElement.md)
- [RemoveElement](IwbContainer_RemoveElement.md)
- [RemoveByIndex](IwbContainer_RemoveByIndex.md)
- [ElementCount](IwbContainer_ElementCount.md)


