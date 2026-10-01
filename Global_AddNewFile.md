# AddNewFile

## Syntax

```pascal
function AddNewFile: Boolean;
function AddNewFile(AIsLight: Boolean): Boolean;
function AddNewFile(AIsLight: Boolean; AIsMedium: Boolean): Boolean;
```

## Description

Prompts for a new plugin name and creates that plugin.

The prompt asks for a filename without an extension. A light plugin is saved as `.esl`. Any other plugin is saved as `.esp`. Omit both flags, or pass False for both, for a normal plugin. Pass True only for `AIsLight` to make a light plugin. Pass True only for `AIsMedium` to make a medium plugin. Do not pass True for both. That combination is rejected.

Cancel the prompt, or enter an empty name, and no file is created.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AIsLight | Boolean | Create a light plugin. Optional. False when omitted |
| AIsMedium | Boolean | Create a medium plugin. Optional. False when omitted. Requires `AIsLight` to be passed as well |

## Returns

True when the plugin was created. False when the prompt is cancelled, the name is empty, or the file is not created.

The new file is not returned. Find it with [FileByName](Global_FileByName.md).

## Example

```pascal
begin
  if AddNewFile(True, False) then
    AddMessage('Created a light plugin');
end;
```

## See Also

- [AddNewFileName](Global_AddNewFileName.md)
- [FileByName](Global_FileByName.md)
