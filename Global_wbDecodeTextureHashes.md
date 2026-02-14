# wbDecodeTextureHashes

## Syntax

```pascal
function wbDecodeTextureHashes: Boolean;
```

## Description

Returns whether texture hash decoding is enabled. When enabled, xEdit will decode texture hash values found in certain record types (like TXST in Fallout 4) back to their original texture paths.

## Parameters

This function takes no parameters.

## Returns

Returns True if texture hash decoding is enabled, False otherwise.

## Example

```pascal
begin
  if wbDecodeTextureHashes then
    AddMessage('Texture hash decoding is enabled')
  else
    AddMessage('Texture hash decoding is disabled');
end;
```

## See Also

- [wbGameMode](Global_wbGameMode.md)
