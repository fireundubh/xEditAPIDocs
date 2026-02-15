# IsInjected

## Syntax

```pascal
function IsInjected(AElement: IwbElement): boolean;
```

## Description

Checks whether the element was created programmatically rather than loaded from disk.

This function retrieves the IsInjected property, which returns true if the element was created at runtime by scripts, xEdit operations, or other programmatic means, rather than being read from the plugin file. Injected elements exist only in memory until the file is saved. Returns false for elements loaded from disk or invalid inputs. Useful for distinguishing between original and runtime-created content.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check if it was injected |

## Returns

Returns true if the element was injected by another plugin, false otherwise.

## Example

```pascal
// Example 1: Identify programmatically created elements
var
  element: IwbElement;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'KWDA');
    if Assigned(element) then begin
      if IsInjected(element) then
        AddMessage(Format('KWDA was created at runtime in %s', [EditorID(e)]))
      else
        AddMessage(Format('KWDA was loaded from disk in %s', [EditorID(e)]));
    end;
  end;
end;

// Example 2: Track injected vs original records
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  injectedCount, originalCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    injectedCount := 0;
    originalCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        if IsInjected(element) then
          Inc(injectedCount)
        else
          Inc(originalCount);
      end;
    end;

    AddMessage(Format('%s: %d original, %d injected elements',
      [EditorID(e), originalCount, injectedCount]));
  end;
end;

// Example 3: Clean up injected elements
var
  keywords: IwbContainer;
  i: integer;
  kwdElement: IwbElement;
  removedCount: integer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      removedCount := 0;
      // Iterate backwards when removing
      for i := ElementCount(keywords) - 1 downto 0 do begin
        kwdElement := ElementByIndex(keywords, i);
        if Assigned(kwdElement) and IsInjected(kwdElement) then begin
          Remove(kwdElement);
          Inc(removedCount);
        end;
      end;
      if removedCount > 0 then
        AddMessage(Format('Removed %d injected keywords from %s',
          [removedCount, EditorID(e)]));
    end;
  end;
end;
```

## See Also

- [IsMaster](IwbMainRecord_IsMaster.md)
- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)


