# AddNewFileName

## Syntax

```pascal
function AddNewFileName(AFileName: string): IwbFile;
function AddNewFileName(AFileName: string; AIsLight: Boolean): IwbFile;
function AddNewFileName(AFileName: string; AIsLight: Boolean; AIsMedium: Boolean): IwbFile;
```

## Description

Creates a plugin with the filename you pass. There is no prompt, and the extension is not changed.

`AFileName` is the filename only, including the extension, such as `MyPlugin.esp`. Omit both flags, or pass False for both, for a normal plugin. Pass True only for `AIsLight` to make a light plugin. Pass True only for `AIsMedium` to make a medium plugin. Do not pass True for both. That combination is rejected.

A filename that is not valid for Windows raises. If that filename already exists under the data path, a message is shown and the call returns nil.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | Filename, including the extension |
| AIsLight | Boolean | Create a light plugin. Optional. False when omitted |
| AIsMedium | Boolean | Create a medium plugin. Optional. False when omitted. Requires `AIsLight` to be passed as well |

## Returns

The new `IwbFile`, or nil when a file of that name already exists under the data path.

## Example

```pascal
var
  f: IwbFile;
begin
  f := AddNewFileName('MyPlugin.esp', False, True);
  if Assigned(f) then
    AddMessage(GetFileName(f));
end;
```

## See Also

- [AddNewFile](Global_AddNewFile.md)
- [FileByName](Global_FileByName.md)
