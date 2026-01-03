# GetRotation

## Syntax

```pascal
function GetRotation(ARecord: IwbMainRecord): TwbVector;
```

## Description

Returns the rotational vector for `ARecord` when the record is a reference

The `x`, `y`, and `z` members of the return type can be accessed as [Single](http:__docwiki.embarcadero.com_Libraries_Rio_en_System.Single.md) fields.

## Example

```pascal
vec3 := GetRotation(e);
x := vec3.x;
y := vec3.y;
z := vec3.z;
```

## See Also

- [GetPosition](IwbMainRecord_GetPosition.md)
