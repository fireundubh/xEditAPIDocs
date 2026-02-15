# ElementByPath

## Syntax

```pascal
function ElementByPath(AContainer: IwbContainer; APath: string): IwbElement;
```

## Description

Navigates through nested containers to find an element at the specified path.

This function accesses the ElementByPath property, which parses the path string and traverses the element hierarchy. Use backslash (\) as the separator for nested elements (e.g., "Model\MODL" finds the MODL element inside the Model struct). The path is resolved relative to the container. Returns nil if any part of the path doesn't exist. More flexible than ElementByName for accessing deeply nested elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search within |
| APath | string | The hierarchical path to the desired element (e.g., `'Model\MODL'`) |

## Returns

Returns the IwbElement at the specified path, or `nil` if the path doesn't exist.

## Example

```pascal
// Example 1: Access nested struct element
var
  modelElement: IwbElement;
  modelPath: string;
begin
  if Assigned(e) then begin
    modelElement := ElementByPath(e, 'Model\MODL');
    if Assigned(modelElement) then begin
      modelPath := GetEditValue(modelElement);
      AddMessage('Model path: ' + modelPath);
    end;
  end;
end;

// Example 2: Navigate deeply nested paths
var
  conditionFunction: IwbElement;
  funcValue: string;
begin
  if Assigned(e) then begin
    // Path through: Conditions array → first condition → CTDA struct → Function field
    conditionFunction := ElementByPath(e, 'Conditions\[0]\CTDA\Function');
    if Assigned(conditionFunction) then begin
      funcValue := GetEditValue(conditionFunction);
      AddMessage('First condition function: ' + funcValue);
    end;
  end;
end;

// Example 3: Accessing array elements by index
var
  keywords: IwbContainer;
  firstKeyword: IwbElement;
  keywordFormID: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      // Access first keyword using array index notation
      firstKeyword := ElementByPath(keywords, '[0]');
      if Assigned(firstKeyword) then begin
        keywordFormID := GetEditValue(firstKeyword);
        AddMessage('First keyword: ' + keywordFormID);
      end;
    end;
  end;
end;

// Example 4: Check if path exists before accessing
var
  scriptElement: IwbElement;
begin
  if Assigned(e) then begin
    scriptElement := ElementByPath(e, 'VMAD\Scripts\[0]\scriptName');
    if Assigned(scriptElement) then
      AddMessage('Has script: ' + GetEditValue(scriptElement))
    else
      AddMessage('No script data found');
  end;
end;
```

## See Also

- [ElementByName](IwbContainer_ElementByName.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementExists](IwbContainer_ElementExists.md)


