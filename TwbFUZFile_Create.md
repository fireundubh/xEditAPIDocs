# TwbFUZFile.Create

## Syntax

```pascal
function TwbFUZFile.Create: TwbFUZFile;
```

## Description

Creates a new FUZ (Facial Animation + Audio) file handler instance.

FUZ files are Bethesda's container format combining lip-sync facial animation data with compressed audio. Used extensively in Skyrim and Fallout games for NPC dialogue, these files package the spoken audio (XWM format) together with phoneme timing data for realistic lip synchronization during conversations.

The FUZ format allows the game engine to efficiently load both the audio and facial animation data as a single unit, ensuring proper synchronization between what NPCs say and their mouth movements.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods for reading, extracting, or repacking FUZ file contents.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbFUZFile` instance ready for loading or creating FUZ audio+animation data.

## Example

```pascal
var
  fuzFile: TwbFUZFile;
begin
  fuzFile := TwbFUZFile.Create;
  try
    // Load existing dialogue FUZ file
    fuzFile.LoadFromFile('Sound\Voice\Skyrim.esm\MaleNord\DialogueWhiterun_0001A234.fuz');

    // Access embedded data
    AddMessage('Audio size: ' + fuzFile.ElementByName('Audio Data Size', True).EditValue);
    AddMessage('Lip data size: ' + fuzFile.ElementByName('Lip Data Size', True).EditValue);

    // Export audio data for editing
    // (Note: actual export would require additional processing)
    AddMessage('Audio format: XWM compressed');
  finally
    fuzFile.Free;
  end;
end;
```

## See Also

- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_SaveToFile](TdfElement_SaveToFile.md)
- [TdfElement_ElementByName](TdfElement_ElementByName.md)
