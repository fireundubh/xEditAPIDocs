# DisplayName

## Syntax

```pascal
function DisplayName(AElement: IwbElement): string;
```

## Description

Returns a user-friendly name suitable for display in interfaces.

This function retrieves the DisplayName property with the True parameter (extended format), which provides a formatted name optimized for UI presentation. For simple elements this may be identical to Name, but for complex elements it may include additional context like values or indices. Returns an empty string for invalid elements. Commonly used in xEdit's tree view and other UI components where clarity is more important than brevity.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose display name to retrieve |

## Returns

Returns the display name of the element as a string. If no specific display name exists, returns the same value as `Name`.

## Example

```pascal
// Example 1: Show user-friendly element names
var
  rec: IwbMainRecord;
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  displayName: string;
begin
  if Assigned(e) then begin
    container := rec;
    AddMessage('Elements in ' + EditorID(e) + ':');
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        displayName := DisplayName(element);
        AddMessage(Format('  %s = %s', [displayName, GetEditValue(element)]));
      end;
    end;
  end;
end;

// Example 2: Compare Name vs DisplayName
var
  rec: IwbMainRecord;
  element: IwbElement;
  elemName, elemDisplay: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'KWDA\[0]');
    if Assigned(element) then begin
      elemName := Name(element);
      elemDisplay := DisplayName(element);
      AddMessage('Name: ' + elemName);
      AddMessage('DisplayName: ' + elemDisplay);
      // Name might be "Keyword [0]", DisplayName adds value context
    end;
  end;
end;

// Example 3: Build UI-friendly element tree
var
  rec: IwbMainRecord;
  conditions: IwbContainer;
  i: integer;
  condition: IwbElement;
  conditionDisplay: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      AddMessage('Condition list for ' + EditorID(e) + ':');
      for i := 0 to ElementCount(conditions) - 1 do begin
        condition := ElementByIndex(conditions, i);
        if Assigned(condition) then begin
          conditionDisplay := DisplayName(condition);
          AddMessage(Format('  Condition %d: %s', [i, conditionDisplay]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [BaseName](IwbElement_BaseName.md)
- [ShortName](IwbElement_ShortName.md)
- [PathName](IwbElement_PathName.md)


