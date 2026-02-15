# Check

## Syntax

```pascal
function Check(AElement: IwbElement): string;
```

## Description

Validates the element and returns any error message found.

This function calls the element's Check method, which performs validation based on the element's definition rules (required fields, value constraints, reference validity, etc.). This is the same validation used by xEdit's "Check for Errors" feature. Returns an empty string if the element is valid or if validation is not applicable. Returns a descriptive error message if validation fails. Use this to verify record integrity before saving.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check for errors |

## Returns

Returns the error message as a string, or an empty string if no error is found.

## Example

```pascal
// Example 1: Validate record before saving
var
  errorMsg: string;
begin
  if Assigned(e) then begin
    errorMsg := Check(e);
    if errorMsg <> '' then
      AddMessage(Format('ERROR in %s: %s', [EditorID(e), errorMsg]))
    else
      AddMessage(Format('%s passes validation', [EditorID(e)]));
  end;
end;

// Example 2: Batch validation with error reporting
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  errorMsg, elementName: string;
  errorCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    errorCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        errorMsg := Check(element);
        if errorMsg <> '' then begin
          elementName := Name(element);
          AddMessage(Format('  [%s] %s', [elementName, errorMsg]));
          Inc(errorCount);
        end;
      end;
    end;

    if errorCount = 0 then
      AddMessage(Format('%s: All elements valid', [EditorID(e)]))
    else
      AddMessage(Format('%s: %d errors found', [EditorID(e), errorCount]));
  end;
end;

// Example 3: Validate and fix common issues
var
  edidElement: IwbElement;
  errorMsg: string;
begin
  if Assigned(e) then begin
    edidElement := ElementByPath(e, 'EDID');
    if Assigned(edidElement) then begin
      errorMsg := Check(edidElement);
      if errorMsg <> '' then begin
        if Pos('required', errorMsg) > 0 then begin
          SetEditValue(edidElement, 'AutoGenEditorID');
          AddMessage(Format('Fixed missing EDID in %s', [EditorID(e)]));
        end else
          AddMessage(Format('Cannot auto-fix: %s', [errorMsg]));
      end;
    end else begin
      // EDID missing entirely
      edidElement := Add(e, 'EDID', True);
      if Assigned(edidElement) then begin
        SetEditValue(edidElement, Format('AutoGen_%s', [IntToHex(FormID(e), 8)]));
        AddMessage(Format('Created EDID for %s', [IntToHex(FormID(e), 8)]));
      end;
    end;
  end;
end;
```

## See Also

- [Assigned - IwbElement](IwbElement_Assigned.md)


