# ObjectToElement

## Syntax

```pascal
function ObjectToElement(AObject: Variant): IwbElement;
```

## Description

Returns an element from `AObject` if the pointer to the object is a compatible `Variant`

The most common use of `ObjectToElement` is the retrieval of elements stored in a `TList`; however, care must be taken to avoid dangling pointer faults.

To avoid dangling pointer faults, follow these guidelines when populating a `TList`:

- All `IwbMainRecord` objects are safe to add to lists; they are always memory resident.
- All member elements of `IwbMainRecord`, such as those inheriting from `IwbSubRecordDef` and `IwbValueDef`, exist only when they have counted references. Otherwise, their pointers may be freed. Note: The pointers to these elements stored in a `TList` are not counted references.

Using a `TList` is not recommended for any elements other than main records.

## Example

```pascal
// Initialize
Refs := TList.Create;

// Process
if ContainsStr('ACHR REFR', Signature(e)) then
	Refs.Add(e);

// Finalize
for i := 0 to Pred(References.Count) do
begin
	ref := ObjectToElement(Refs[i]);
  AddMessage(Name(ref));
end;

Refs.Free;
```
