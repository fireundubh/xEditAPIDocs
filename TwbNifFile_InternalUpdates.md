# InternalUpdates

## Syntax

```pascal
property InternalUpdates: Boolean;
```

Access via: `nifFile.InternalUpdates` (read) or `nifFile.InternalUpdates := value` (write)

## Description

Gets or sets whether save-time header maintenance is enabled. The default is True.

When True, saving refreshes the header (block count, block type table, and related header fields). `nfoCollapseLinkArrays` removes None links only while this is also True. Insert, delete, and move still remap block indices when this is False.

Set it False only when you intend to skip that header update. Turn it back on before saving if the header should match the blocks.

This is a read/write property.

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
