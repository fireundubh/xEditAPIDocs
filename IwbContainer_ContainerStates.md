# ContainerStates

## Syntax

```pascal
function ContainerStates(AContainer: IwbContainer): byte;
```

## Description

Returns the internal container state flags as a bitmask (e.g., initialized, references built.)

The returned byte value contains bit flags representing various states of the container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve state flags from |

## Returns

Returns a byte value containing bitmask flags representing the container's state.

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
  states: byte;
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
  states: byte;
  isInitialized, hasRefs, wasEmpty: boolean;
begin
  container := e;
  if Assigned(container) then begin
    states := ContainerStates(container);

    isInitialized := (states and (1 shl csInitDone)) <> 0;
    hasRefs := (states and (1 shl csRefsBuild)) <> 0;
    wasEmpty := (states and (1 shl csAsCreatedEmpty)) <> 0;

    AddMessage('Container state:');
    AddMessage(Format('  Initialized: %s', [BoolToStr(isInitialized, True)]));
    AddMessage(Format('  References built: %s', [BoolToStr(hasRefs, True)]));
    AddMessage(Format('  Created empty: %s', [BoolToStr(wasEmpty, True)]));
  end;
end;

// Example 3: Wait for initialization before accessing container
var
  container: IwbContainer;
  states: byte;
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


