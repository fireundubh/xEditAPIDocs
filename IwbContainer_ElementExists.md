# ElementExists

## Syntax

```pascal
function ElementExists(AContainer: IwbContainer; APath: string): boolean;
```

## Description

Checks whether an element exists at the specified path within the container.

This function accesses the ElementExists property, which performs a path lookup without returning the element itself. More efficient than ElementByPath when you only need to check existence. The path uses backslash separators for nested elements. Returns false if any part of the path doesn't exist or for invalid inputs. Useful for conditional logic before accessing potentially missing elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search in |
| APath | string | The element path to check for existence |

## Returns

Returns true if the element exists at the specified path, false otherwise.

## Example

```pascal
// Example 1: Check before accessing optional element
var
  modelPath: string;
begin
  if Assigned(e) then begin
    if ElementExists(e, 'Model\MODL') then begin
      modelPath := GetElementEditValue(e, 'Model\MODL');
      AddMessage('Model path: ' + modelPath);
    end else
      AddMessage('No model data');
  end;
end;

// Example 2: Validate required fields before processing
var
  canProcess: boolean;
begin
  if Assigned(e) then begin
    canProcess := ElementExists(e, 'EDID') and
                  ElementExists(e, 'FULL') and
                  ElementExists(e, 'DATA');

    if canProcess then
      AddMessage('Record has all required fields')
    else begin
      AddMessage('Missing required fields:');
      if not ElementExists(e, 'EDID') then AddMessage('  - EDID');
      if not ElementExists(e, 'FULL') then AddMessage('  - FULL');
      if not ElementExists(e, 'DATA') then AddMessage('  - DATA');
    end;
  end;
end;

// Example 3: Check nested array elements
var
  hasConditions, hasFirstCondition: boolean;
begin
  if Assigned(e) then begin
    hasConditions := ElementExists(e, 'Conditions');
    if hasConditions then begin
      hasFirstCondition := ElementExists(e, 'Conditions\[0]');
      if hasFirstCondition then
        AddMessage('Has at least one condition')
      else
        AddMessage('Conditions array exists but is empty');
    end else
      AddMessage('No conditions array');
  end;
end;

// Example 4: Conditional script data access
var
  scriptName: string;
begin
  if Assigned(e) then begin
    // Check if script data exists before accessing
    if ElementExists(e, 'VMAD\Scripts\[0]\scriptName') then begin
      scriptName := GetElementEditValue(e, 'VMAD\Scripts\[0]\scriptName');
      AddMessage('First script: ' + scriptName);
    end else if ElementExists(e, 'VMAD') then
      AddMessage('Has VMAD but no scripts')
    else
      AddMessage('No script data');
  end;
end;
```

## See Also

- [ElementByPath](IwbContainer_ElementByPath.md)
- [ElementByName](IwbContainer_ElementByName.md)
- [IndexOf](IwbContainer_IndexOf.md)


