# wbOutputPath

## Syntax

```pascal
function wbOutputPath: string;
```

Assign it as well. The assignment takes a string and returns nothing.

```pascal
wbOutputPath := 'C:\Output\';
```

## Description

Reads or sets the path where xEdit writes generated files such as LOD meshes and textures.

## Parameters

The function takes no parameters. The assignment takes the new path.

## Returns

The function returns the output directory path. The assignment returns nothing.

## Example

```pascal
begin
  AddMessage(wbOutputPath);
  wbOutputPath := 'C:\Output\';
end;
```

## See Also

- [wbDataPath](Global_wbDataPath.md)
- [wbTempPath](Global_wbTempPath.md)
