# TdfElement.LoadFromResource

## Syntax

```pascal
// Two-parameter version
procedure LoadFromResource(const aContainerName, aFileName: string);

// One-parameter version
procedure LoadFromResource(const aFileName: string);
```

## Description

Loads binary data from a resource archive (BSA/BA2) by extracting and deserializing the file.

The LoadFromResource method provides two overloads for loading files from game archives:

1. The two-parameter version explicitly specifies both the archive name and the file path within it.
2. The one-parameter version uses a callback (dfResourceGetDataCallback) to resolve the file from available archives.

This is particularly useful for loading game assets directly from BSA/BA2 archives without extracting them to disk first. The callback approach allows integration with xEdit's resource management system which handles archive priority and file lookup.

Any existing data in the element is replaced with the newly loaded resource data.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aContainerName | string | (Two-parameter version) Name of the BSA/BA2 archive file |
| aFileName | string | File path within the archive (or just file path for one-parameter version) |

## Returns

This method does not return a value.

## Example

```pascal
var
    nifFile: TwbNifFile;
begin
    nifFile := TwbNifFile.Create;
    try
        // Load from specific archive
        nifFile.LoadFromResource('Skyrim - Meshes0.bsa', 'meshes\actors\character\character.nif');

        // Or use callback-based resolution
        nifFile.LoadFromResource('meshes\actors\character\character.nif');

        AddMessage('Loaded NIF from archive');
        AddMessage('Block Count: ' + IntToStr(nifFile.BlocksCount));
    finally
        nifFile.Free;
    end;
end;
```

## See Also

- [TdfElement.LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement.LoadFromData](TdfElement_LoadFromData.md)
- [TdfElement.SaveToFile](TdfElement_SaveToFile.md)
