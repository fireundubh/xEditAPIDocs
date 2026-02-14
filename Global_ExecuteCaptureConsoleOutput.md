# ExecuteCaptureConsoleOutput

## Syntax

```pascal
function ExecuteCaptureConsoleOutput(ACommandLine: string): string;
```

## Description

Executes a command-line application and captures its console output. This function runs the specified command and returns all text written to the standard output stream, allowing scripts to interact with external programs.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ACommandLine | string | The command line to execute, including program path and arguments |

## Returns

Returns a string containing all console output produced by the executed command.

## Example

```pascal
var
  output: string;
begin
  output := ExecuteCaptureConsoleOutput('cmd.exe /c dir "' + DataPath + 'Meshes" /b');
  AddMessage('Files in Meshes directory:');
  AddMessage(output);
end;
```

## See Also

- [AddMessage](Global_AddMessage.md)
