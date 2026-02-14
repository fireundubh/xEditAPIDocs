# ResourceExists

## Syntax

```pascal
function ResourceExists(AFileName: String): Boolean;
```

## Description

Returns `True` if any loaded resource contains a file matching `AFileName`, and `False` otherwise

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | String | The file name to search for in loaded resources |

## Returns

Returns `True` if the file exists in any loaded resource, `False` otherwise.

## Example

```pascal
if ResourceExists(aFileName) then
  AddMessage(aFileName + ' exists in a resource!');
```

