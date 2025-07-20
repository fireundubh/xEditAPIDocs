# AddNewFile

## Syntax

```pascal
function AddNewFile(AIsESL: Boolean = False): IwbFile;
```

## Description

Appends a blank plugin to the tree view, prompts the user for a file name, and returns the file. If the user cancels the prompt, `Nil` will be returned.

`AIsESL` is an optional argument and defaults to `False`, but when `True`, the new plugin will be created as an ESL-flagged plugin with the `.esl` extension.

**Note:** The new plugin will not exist in the file system until the plugin is saved.

## Example

```pascal
f := AddNewFile;

if not Assigned(f) then
	Exit;
  
AddMessage('File created with name: ' + GetFileName(f));
```

## See Also

- [AddNewFileName - Global](Global_AddNewFileName.md)
