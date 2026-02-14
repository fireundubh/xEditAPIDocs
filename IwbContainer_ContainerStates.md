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
if ContainerStates(GetFile(e)) and (1 shl csRefsBuild) = 0 then
begin
    AddMessage('Skipping record, references are not built for file');
    Exit;
end;
```

## See Also

- [IsSorted](IwbContainer_IsSorted.md)


