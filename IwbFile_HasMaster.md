# HasMaster

## Syntax

```pascal
function HasMaster(AFile: IwbFile; AFileName: String): Boolean;
```

## Description

Checks whether the file's master list contains the specified filename.

This function calls the HasMaster method, which searches the file's master list for a file with the given name. The search is case-insensitive and matches against filenames in the master header entries. Returns true if found, false otherwise. Useful for checking dependencies before adding records that reference another file's content.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check for master dependencies |
| AFileName | String | The name of the master file to look for |

## Returns

Returns `True` if `AFile` depends on a master file named `AFileName`, and `False` otherwise.

## Example

```pascal
f := FileByName('Dawnguard.esm');
if HasMaster(f, 'Skyrim.esm') then
  AddMessage('Dawnguard.esm depends on Skyrim.esm');
```

