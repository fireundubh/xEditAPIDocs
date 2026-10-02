# Add

## Syntax

```pascal
function Add(AContainer: IwbContainer; ANameOrSignature: string; ASilent: boolean): IwbElement;
```

## Description

Creates and adds a new child element to the container by name or signature.

On a record or subrecord struct, `ANameOrSignature` is a member name or a 4-character signature. If that member is already present, the existing element is returned; otherwise it is created. On an array, a new element is appended. On a group, the name must start with a signature that group can contain.

`ASilent` is required. It is not a notification switch. On a group, `True` allocates a new FormID without prompting and `False` asks for one. Adding a worldspace cell with `ASilent` set to `True` requires the name `CELL[P]` or `CELL[x,y]`. On records and arrays the flag is ignored, except when a child record is forwarded to a child group.

Returns the new or existing element, or nil if nothing was added. If the argument is not a container, the result is unassigned.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to add the element to |
| ANameOrSignature | string | The name or signature of the element to add |
| ASilent | boolean | Required. On a group, True assigns a FormID without prompting; False prompts. Ignored for most record and array adds |

## Returns

Returns the new or existing element, or nil if nothing was added. If the argument is not a container, the result is unassigned.

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
            SetElementEditValues(condition, 'CTDA\Type', '10000000');
            SetElementEditValues(condition, 'CTDA\Comparison Value', IntToStr(i));
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
      effect := Add(effects, 'Effect', False);
      if Assigned(effect) then begin
        SetElementEditValues(effect, 'EFID', 'RestoreHealth');
        SetElementEditValues(effect, 'EFIT\Magnitude', '25');
        SetElementEditValues(effect, 'EFIT\Duration', '0');
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


