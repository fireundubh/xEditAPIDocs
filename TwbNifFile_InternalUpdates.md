# InternalUpdates

## Syntax

```pascal
function InternalUpdates(ANifFile: TwbNifFile): Boolean; // Get
procedure InternalUpdates(ANifFile: TwbNifFile; AValue: Boolean); // Set
```

## Description

Gets or sets whether internal automatic updates are enabled. When enabled, the NIF file automatically maintains internal data structures and references when blocks are added, removed, or modified.

Internal updates include:
- Updating block reference indices when blocks are inserted or deleted
- Maintaining the header's block count
- Updating link arrays and reference counts
- Renumbering blocks to maintain consistency

Setting this to False can improve performance when making many modifications, but you must manually ensure data consistency. It's recommended to disable internal updates only during batch operations, then re-enable them before saving.

Default value is True.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ANifFile | TwbNifFile | The NIF file object |
| AValue | Boolean | The value to set (for setter) |

## Returns

Returns the current internal updates state as Boolean (for getter).

## Example

```pascal
var
  nif: TwbNifFile;
  i: Integer;
  block: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\ruins\ruinspot01.nif');

    // Disable internal updates for batch operations
    nif.InternalUpdates := False;
    try
      // Perform many modifications
      for i := 0 to nif.BlocksCount - 1 do begin
        block := nif.Blocks[i];
        // Modify blocks...
      end;
    finally
      // Re-enable internal updates
      nif.InternalUpdates := True;
    end;

    // Updates are now applied
    nif.SaveToFile('meshes\clutter\ruins\ruinspot01_modified.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_Options](TwbNifFile_Options.md)
- [TwbNifFile_AddBlock](TwbNifFile_AddBlock.md)
- [TwbNifFile_InsertBlock](TwbNifFile_InsertBlock.md)
- [TdfElement_BeginUpdate](TdfElement_BeginUpdate.md)
