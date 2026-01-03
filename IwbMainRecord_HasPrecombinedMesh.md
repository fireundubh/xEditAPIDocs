# HasPrecombinedMesh

## Syntax

```pascal
function HasPrecombinedMesh(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is a Fallout 4 reference that has precombined mesh data

## Example

```pascal
if HasPrecombinedMesh(e) then
	AddMessage(Name(e) + ' has precombined mesh data');
```

## See Also

- [PrecombinedMesh](IwbMainRecord_PrecombinedMesh.md)


