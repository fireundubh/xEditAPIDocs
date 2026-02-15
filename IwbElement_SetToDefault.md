# SetToDefault

## Syntax

```pascal
procedure SetToDefault(AElement: IwbElement);
```

## Description

Resets the element to its default value and ensures required substructures exist.

This function calls the element's SetToDefault method, which restores the element's data to the default value specified in its definition and creates any missing required child elements. Useful for initializing new records or resetting corrupted data. The exact behavior depends on the element type: simple values reset to their default, containers ensure required children exist. The element must be editable.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to reset to default |

## Example

```pascal
// Example 1: Initialize new record with default values
var
  rec: IwbMainRecord;
  dataElement: IwbElement;
begin
  if Assigned(e) then begin
    dataElement := Add(rec, 'DATA', true);
    if Assigned(dataElement) then begin
      SetToDefault(dataElement);
      AddMessage(Format('Initialized DATA with defaults in %s', [EditorID(e)]));
    end;
  end;
end;

// Example 2: Reset corrupted element to defaults
var
  rec: IwbMainRecord;
  valueElement: IwbElement;
  oldValue: string;
begin
  if Assigned(e) then begin
    valueElement := ElementByPath(rec, 'DATA\Value');
    if Assigned(valueElement) then begin
      oldValue := GetEditValue(valueElement);
      SetToDefault(valueElement);
      AddMessage(Format('%s: Reset value from "%s" to default "%s"',
        [EditorID(rec), oldValue, GetEditValue(valueElement)]));
    end;
  end;
end;

// Example 3: Ensure required child elements exist
var
  rec: IwbMainRecord;
  container: IwbContainer;
  modelElement: IwbElement;
begin
  if Assigned(e) then begin
    container := rec;
    modelElement := ElementByPath(container, 'Model');
    if Assigned(modelElement) then begin
      // SetToDefault creates any missing required child elements
      SetToDefault(modelElement);
      AddMessage(Format('Ensured Model structure complete in %s', [EditorID(e)]));
    end else begin
      modelElement := Add(container, 'Model', true);
      if Assigned(modelElement) then begin
        SetToDefault(modelElement);
        AddMessage(Format('Created and initialized Model in %s', [EditorID(e)]));
      end;
    end;
  end;
end;
```

## See Also

- [Check](IwbElement_Check.md)


