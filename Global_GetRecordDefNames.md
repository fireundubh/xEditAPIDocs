# GetRecordDefNames

## Syntax

```pascal
procedure GetRecordDefNames(AList: TStrings);
```

## Description

Populates `AList` with names of all record definitions for the current game mode

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AList | TStrings | The string list to populate with record definition names |

## Example

```pascal
ls := TStringList.Create;

GetRecordDefNames(ls);

for i := 0 to Pred(ls.Count) do
  AddMessage(ls[i]);

ls.Free;

// Example Output:
// ----------------------------
// ACHR - Placed NPC
// ACTI - Activator
// TACT - Talking Activator
// ALCH - Ingestible
// ...
```

