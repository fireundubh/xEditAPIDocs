# ScriptProcessSignatures

## Syntax

```pascal
ScriptProcessSignatures: string;
```

Assign it. Do not call it, and do not read it back. The host accepts the write and does not keep a script variable of this name. Do not declare a variable of this name. A declared variable takes the assignment, and the host filter is left unchanged.

## Description

Limits which selected main records are passed to `Process`.

xEdit clears this at the start of Apply Script, before `Initialize`. Set it in `Initialize`. A value set in `Process` only affects records visited after that assignment. A value set in `Finalize` is too late.

The value is a list of record signatures. Commas, spaces, tabs, and line breaks separate entries, and spaces around an entry are removed. A double quote starts a quoted entry: `"WEAP"` is the signature `WEAP`, and `" WEAP "` is accepted after the surrounding spaces are removed. Each entry must be exactly four characters, such as `WEAP` or `NPC_`. The host stores the list in uppercase. A record matches when its signature appears in that list. `Process` is not called for a main record that does not match.

An empty string, or a string made only of spaces, tabs, or line breaks, clears the filter. Every selected main record is then passed to `Process`.

An entry that is not four characters stops the script. A trailing comma, or two commas in a row, counts as an empty entry and stops the script. The message names the rejected entry, for example `ScriptProcessSignatures expects a comma separated list of 4 character signatures. The signature "WEAPX" is not a valid candidate.` The host's message names commas only. Spaces still separate entries.

The filter applies only to main records (`etMainRecord`). Other element types are not matched against this list. By default, `Process` is only called for main records.

## Parameters

This is not a function. The assignment takes one string.

| Name | Type | Description |
|------|------|-------------|
| Value | string | Comma-separated or space-separated four-character signatures. Empty, or only spaces, tabs, or line breaks, clears the filter |

## Returns

Nothing. A bad entry aborts the script with an error.

## Example

```pascal
function Initialize: Integer;
begin
  ScriptProcessSignatures := 'WEAP,ARMO';
  Result := 0;
end;

function Process(e: IInterface): Integer;
begin
  if Assigned(e) then
    AddMessage(Signature(e));
  Result := 0;
end;
```

## See Also

- [ElementType](IwbElement_ElementType.md)
- [GroupBySignature](IwbFile_GroupBySignature.md)
- [Signature](IwbMainRecord_Signature.md)
