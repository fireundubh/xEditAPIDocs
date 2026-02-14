# wbFormIDErrorCheckUnlock

## Syntax

```pascal
function wbFormIDErrorCheckUnlock: Integer;
```

## Description

Unlocks FormID error checking, re-enabling validation of FormID references. This function decrements the internal lock counter and returns the new count. Error checking resumes when the lock count reaches zero.

## Parameters

This function takes no parameters.

## Returns

Returns an Integer representing the new FormID error check lock count.

## Example

```pascal
var
  lockCount: Integer;
begin
  wbFormIDErrorCheckLock;

  try
    // Perform operations without FormID validation
    AddMessage('Processing without FormID checks');
  finally
    lockCount := wbFormIDErrorCheckUnlock;
    AddMessage('FormID checking unlocked, count: ' + IntToStr(lockCount));
  end;
end;
```

## See Also

- [wbFormIDErrorCheckLock](IwbResource_wbFormIDErrorCheckLock.md)
