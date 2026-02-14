# wbLoadBSAs

## Syntax

```pascal
function wbLoadBSAs: Boolean;
```

## Description

Returns whether BSA (Bethesda Softworks Archive) files are configured to be loaded automatically. When enabled, xEdit will load and provide access to resources stored in BSA and BA2 archive files.

## Parameters

This function takes no parameters.

## Returns

Returns True if BSA loading is enabled, False otherwise.

## Example

```pascal
begin
  if wbLoadBSAs then
    AddMessage('BSA archives are being loaded')
  else
    AddMessage('BSA archives are not loaded');
end;
```

## See Also

- [ResourceExists](IwbContainer_ResourceExists.md)
- [ResourceOpenData](IwbContainer_ResourceOpenData.md)
