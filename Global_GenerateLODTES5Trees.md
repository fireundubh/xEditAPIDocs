# GenerateLODTES5Trees

## Syntax

```pascal
procedure GenerateLODTES5Trees(AMainRecord: IwbMainRecord);
```

## Description

Generates tree Level of Detail (LOD) data for Skyrim (TES5) worldspaces. This function creates distant tree LOD meshes and billboards for the specified worldspace record. It only operates when the current game mode is a Skyrim variant.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AMainRecord | IwbMainRecord | The worldspace main record to generate tree LOD for |

## Returns

This function does not return a value.

## Example

```pascal
var
  worldspace: IwbMainRecord;
begin
  worldspace := RecordByEditorID('Tamriel');

  if wbIsSkyrim then begin
    GenerateLODTES5Trees(worldspace);
    AddMessage('Tree LOD generation started for Tamriel');
  end;
end;
```

## See Also

- [GenerateLODTES5Objects](Global_GenerateLODTES5Objects.md)
- [GenerateLODTES4](Global_GenerateLODTES4.md)
