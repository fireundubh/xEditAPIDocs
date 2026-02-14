# PrecombinedMesh

## Syntax

```pascal
function PrecombinedMesh(ARecord: IwbMainRecord): string;
```

## Description

Returns the precombined mesh file path for `ARecord` if record is a Fallout 4 reference but not a placed actor

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The Fallout 4 reference record to get the precombined mesh path from |

## Returns

Returns the file path to the precombined mesh as a string.

## Example

```pascal
if HasPrecombinedMesh(e) then
	AddMessage(Name(e) + ' has precombined mesh data at: ' + PrecombinedMesh(e));
```

## See Also

- [HasPrecombinedMesh](IwbMainRecord_HasPrecombinedMesh.md)


