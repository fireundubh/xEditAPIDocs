# GenerateLODTES4

## Syntax

```pascal
procedure GenerateLODTES4(AMainRecord: IwbMainRecord);
```

## Description

Generates Level of Detail (LOD) data for Oblivion (TES4) worldspaces. This function creates distant land LOD meshes and textures for the specified worldspace record, but only when the current game mode is Oblivion (gmTES4).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AMainRecord | IwbMainRecord | The worldspace main record to generate LOD for |

## Returns

This function does not return a value.

## Example

```pascal
var
  worldspace: IwbMainRecord;
begin
  worldspace := RecordByEditorID('Tamriel');

  if wbGameMode = gmTES4 then begin
    GenerateLODTES4(worldspace);
    AddMessage('LOD generation started for Tamriel');
  end;
end;
```

## See Also

- [GenerateLODTES5Trees](Global_GenerateLODTES5Trees.md)
- [GenerateLODTES5Objects](Global_GenerateLODTES5Objects.md)
