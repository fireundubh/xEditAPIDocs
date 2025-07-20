# PrecombinedMesh

## Syntax

```pascal
function PrecombinedMesh(ARecord: IwbMainRecord): string;
```

## Description

Returns the precombined mesh file path for `ARecord` if record is a Fallout 4 reference but not a placed actor

## Example

```pascal
if HasPrecombinedMesh(e) then
	AddMessage(Name(e) + ' has precombined mesh data at: ' + PrecombinedMesh(e));
```

## See Also

- [HasPrecombinedMesh - IwbMainRecord](IwbMainRecord_HasPrecombinedMesh.md)
