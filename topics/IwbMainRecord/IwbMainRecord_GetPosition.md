# GetPosition

## Syntax

```pascal
function GetPosition(ARecord: IwbMainRecord): TwbVector;
```

## Description

Returns the positional vector for `ARecord` when the record is a reference

The `x`, `y`, and `z` members of the return type can be accessed as [Single](http:__docwiki.embarcadero.com_Libraries_Rio_en_System.Single.md) fields.

## Example

```pascal
vec3 := GetPosition(e);
x := vec3.x;
y := vec3.y;
z := vec3.z;
```

## See Also

- [GetRotation - IwbMainRecord](IwbMainRecord_GetRotation.md)
