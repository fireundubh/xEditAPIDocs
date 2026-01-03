# ResourceExists

## Syntax

```pascal
function ResourceExists(AFileName: String): Boolean;
```

## Description

Returns `True` if any loaded resource contains a file matching `AFileName`, and `False` otherwise

## Example

```pascal
if ResourceExists(aFileName) then
  AddMessage(aFileName + ' exists in a resource!');
```

