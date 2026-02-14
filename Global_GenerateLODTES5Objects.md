# GenerateLODTES5Objects

## Syntax

```pascal
procedure GenerateLODTES5Objects(AMainRecord: IwbMainRecord);
```

## Description

Generates object Level of Detail (LOD) data for Skyrim (TES5) worldspaces. This function creates distant object LOD meshes for the specified worldspace record. It only operates when the current game mode is a Skyrim variant.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AMainRecord | IwbMainRecord | The worldspace main record to generate object LOD for |

## Returns

This function does not return a value.

## Example

```pascal
var
  worldspace: IwbMainRecord;
begin
  worldspace := RecordByEditorID('Tamriel');

  if wbIsSkyrim then begin
    GenerateLODTES5Objects(worldspace);
    AddMessage('Object LOD generation started for Tamriel');
  end;
end;
```

## See Also

- [GenerateLODTES5Trees](Global_GenerateLODTES5Trees.md)
- [GenerateLODTES4](Global_GenerateLODTES4.md)
