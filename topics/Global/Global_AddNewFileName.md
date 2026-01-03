# AddNewFileName

## Syntax

```pascal
function AddNewFileName(AFileName: string; AIsESL: Boolean = False): IwbFile;
```

## Description

Appends a blank plugin to the tree view named `AFileName` and returns the file. If the user cancels the prompt, `Nil` will be returned.

`AIsESL` is an optional argument and defaults to `False`, but when `True`, the new plugin will be created as an ESL-flagged plugin with the `.esl` extension.

**Note:** The new plugin will not exist in the file system until the plugin is saved.

## Example

```pascal
f := AddNewFileName('MyPlugin.esp');

if not Assigned(f) then
	Exit;
  
AddMessage('File created with name: ' + GetFileName(f));
```

## See Also

- [AddNewFile](Global_AddNewFile.md)
