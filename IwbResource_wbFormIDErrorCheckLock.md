# wbFormIDErrorCheckLock

## Syntax

```pascal
function wbFormIDErrorCheckLock: Integer;
```

## Description

Locks FormID error checking, preventing validation of FormID references. This function increments an internal counter and returns the new lock count. Error checking is suspended when the lock count is greater than zero.

## Parameters

This function takes no parameters.

## Returns

Returns an Integer representing the new FormID error check lock count.

## Example

```pascal
var
  lockCount: Integer;
begin
  // Disable FormID error checking temporarily
  lockCount := wbFormIDErrorCheckLock;

  try
    // Perform operations that might trigger FormID errors
    AddMessage('FormID checking locked, count: ' + IntToStr(lockCount));
  finally
    // Always unlock when done
    wbFormIDErrorCheckUnlock;
  end;
end;
```

## See Also

- [wbFormIDErrorCheckUnlock](IwbResource_wbFormIDErrorCheckUnlock.md)
