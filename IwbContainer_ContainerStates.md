# ContainerStates

## Syntax

```pascal
function ContainerStates(AContainer: IwbContainer): Word;
```

## Description

Returns the internal container state flags as a bitmask (e.g., initialized, references built.)

The result is a Word, not a byte. Flags past bit 7 are preserved. If the argument is not a container, the result is unassigned rather than 0. The constants below are the ones a script can name; other flags may still be set in the mask.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve state flags from |

## Returns

A Word bitmask of container state flags, or unassigned if the argument is not a container.

## Constants

- `csInit`
- `csInitOnce`
- `csInitDone`
- `csInitializing`
- `csRefsBuild`
- `csAsCreatedEmpty`

## Example

```pascal
// Example 1: Check if references are built before processing
var
  plugin: IwbFile;
  states: integer;
begin
  plugin := GetFile(e);
  if Assigned(plugin) then begin
    states := ContainerStates(plugin);
    if (states and (1 shl csRefsBuild)) = 0 then begin
      AddMessage('Skipping record, references are not built for file');
      Exit;
    end;

    // Safe to process references now
    if Assigned(e) then
      AddMessage(Format('Processing %s with references', [EditorID(e)]));
  end;
end;

// Example 2: Check multiple state flags
var
  container: IwbContainer;
  states: integer;
  isInitialized, hasRefs, wasEmpty: boolean;
begin
  container := e;
  if Assigned(container) then begin
    states := ContainerStates(container);

    isInitialized := (states and (1 shl csInitDone)) <> 0;
    hasRefs := (states and (1 shl csRefsBuild)) <> 0;
    wasEmpty := (states and (1 shl csAsCreatedEmpty)) <> 0;

    AddMessage('Container state:');
    if isInitialized then
      AddMessage('  Initialized: True')
    else
      AddMessage('  Initialized: False');
    if hasRefs then
      AddMessage('  References built: True')
    else
      AddMessage('  References built: False');
    if wasEmpty then
      AddMessage('  Created empty: True')
    else
      AddMessage('  Created empty: False');
  end;
end;

// Example 3: Wait for initialization before accessing container
var
  container: IwbContainer;
  states: integer;
  isInitializing: boolean;
begin
  if Assigned(e) then begin
    container := e;
    states := ContainerStates(container);

    isInitializing := (states and (1 shl csInitializing)) <> 0;
    if isInitializing then begin
      AddMessage('Container is still initializing, deferring access');
      Exit;
    end;

    AddMessage('Container ready for access');
  end;
end;
```

## See Also

- [IsSorted](IwbContainer_IsSorted.md)


