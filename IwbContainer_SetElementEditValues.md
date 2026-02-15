# SetElementEditValues

## Syntax

```pascal
procedure SetElementEditValues(AContainer: IwbContainer; APath: string; AValue: string);
```

## Description

Changes the edit value of an element in the container identified by the specified path.

This procedure modifies the human-readable edit value of an element. The path parameter uses slash notation to navigate to nested elements. The value is converted from string to the appropriate type for the target element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container containing the element to modify |
| APath | string | The element path to the value |
| AValue | string | The new edit value to set |

## Example

```pascal
// Example 1: Update nested struct values
var
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      SetElementEditValues(e, 'DATA\Value', '500');
      SetElementEditValues(e, 'DATA\Weight', '12.5');
      SetElementEditValues(e, 'DATA\Health', '100');
      AddMessage('Updated DATA fields');
    finally
      EndUpdate(e);
    end;
  end;
end;

// Example 2: Batch update record properties
var
begin
  if Assigned(e) then begin
    BeginUpdate(rec);
    try
      SetElementEditValues(e, 'EDID', 'MyNewItem');
      SetElementEditValues(e, 'FULL', 'My New Item Name');
      SetElementEditValues(e, 'Model\MODL', 'meshes\armor\myarmor.nif');
      AddMessage('Updated basic record fields');
    finally
      EndUpdate(e);
    end;
  end;
end;

// Example 3: Update array element value
var
  keywords: IwbContainer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) > 0) then begin
      SetElementEditValues(e, 'KWDA\[0]', '00012345');
      AddMessage('Updated first keyword');
    end;
  end;
end;

// Example 4: Update condition values
var
  conditions: IwbContainer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) and (ElementCount(conditions) > 0) then begin
      BeginUpdate(conditions);
      try
        SetElementEditValues(e, 'Conditions\[0]\CTDA\Type', '10000000');
        SetElementEditValues(e, 'Conditions\[0]\CTDA\Comparison Value', '5');
        SetElementEditValues(e, 'Conditions\[0]\CTDA\Function', 'GetLevel');
        AddMessage('Updated first condition');
      finally
        EndUpdate(conditions);
      end;
    end;
  end;
end;
```

## See Also

- [GetElementEditValues](IwbContainer_GetElementEditValues.md)
- [SetElementNativeValues](IwbContainer_SetElementNativeValues.md)
- [SetEditValue](IwbElement_SetEditValue.md)


