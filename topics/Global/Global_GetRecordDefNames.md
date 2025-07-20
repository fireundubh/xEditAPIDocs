# GetRecordDefNames

## Syntax

```pascal
procedure GetRecordDefNames(AList: TStrings);
```

## Description

Populates `AList` with names of all record definitions for the current game mode

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
