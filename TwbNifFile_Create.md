# Create

## Syntax

```pascal
function Create(): TwbNifFile;
```

## Description

Creates a new empty TwbNifFile object. This is the constructor for the NIF file class and must be called before loading or creating NIF data.

The newly created TwbNifFile is empty and uninitialized. After creation, you can either:
- Load an existing NIF file using LoadFromFile, LoadFromData, or LoadFromResource
- Create a new NIF structure by setting the NifVersion and adding blocks

Always use try-finally to ensure the TwbNifFile object is properly freed when you're done with it.

## Parameters

None.

## Returns

Returns a new TwbNifFile instance.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
begin
  // Create a new NIF file object
  nif := TwbNifFile.Create;
  try
    // Load existing NIF
    nif.LoadFromFile('meshes\clutter\bucket01.nif');
    AddMessage('Loaded NIF with ' + IntToStr(nif.BlocksCount) + ' blocks');

    // Process the NIF...
    rootNode := nif.RootNode;
    if Assigned(rootNode) then
      AddMessage('Root node: ' + rootNode.ElementByPath['Name'].EditValue);

    // Save modified NIF
    nif.SaveToFile('meshes\clutter\bucket01_modified.nif');
  finally
    // Always free the object
    nif.Free;
  end;
end;
```

## Example (Creating New NIF)

```pascal
var
  nif: TwbNifFile;
  header: TwbNifBlock;
  rootNode: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    // Set version for Skyrim SE
    nif.NifVersion := nfSSE;

    // Add root node
    rootNode := nif.AddBlock('NiNode');
    rootNode.ElementByPath['Name'].EditValue := 'Scene Root';

    AddMessage('Created new NIF structure');
    nif.SaveToFile('meshes\test\new_nif.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_NifVersion](TwbNifFile_NifVersion.md)
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_SaveToFile](TdfElement_SaveToFile.md)
- [TwbNifFile_AddBlock](TwbNifFile_AddBlock.md)
