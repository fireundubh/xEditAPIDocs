# ExtraDataByType

## Syntax

```pascal
function ExtraDataByType(ABlockType: string): TwbNifBlock;
function ExtraDataByType(ABlockType: string; AInherited: Boolean): TwbNifBlock;
```

**Access via:** `block.ExtraDataByType(ABlockType)` or `block.ExtraDataByType(ABlockType, Inherited)`

## Description

Finds and returns the first extra data block of a specific type attached to this block. Returns nil if no matching extra data is found.

This is a convenience method for finding a single extra data block when you expect only one or only need the first match. It's commonly used to locate specific metadata blocks like BSXFlags or behavior graph data.

The method supports both exact type matching and inheritance checking. When inheritance is enabled, it returns the first extra data block that is of the specified type or inherits from it.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockType | string | The extra data type to search for |
| AInherited | Boolean | Optional. If True, include inherited types; if False, exact match only. Default is False |

## Returns

Returns the first matching extra data block, or nil if none found.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
  bsxFlags: TwbNifBlock;
  behaviorGraph: TwbNifBlock;
  flagValue: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\furniture\noble\thronenoble01.nif');

    rootNode := nif.RootNode;

    if Assigned(rootNode) then begin
      // Look for BSXFlags
      bsxFlags := rootNode.ExtraDataByType('BSXFlags', False);

      if Assigned(bsxFlags) then begin
        flagValue := bsxFlags.NativeValues['Integer Data'];
        AddMessage('BSXFlags: ' + IntToStr(flagValue));
      end else
        AddMessage('No BSXFlags found');

      // Look for behavior graph
      behaviorGraph := rootNode.ExtraDataByType('BSBehaviorGraphExtraData', False);

      if Assigned(behaviorGraph) then
        AddMessage('Has behavior graph: ' + behaviorGraph.EditValues['Name']);
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_ExtraDatasByType](TwbNifBlock_ExtraDatasByType.md)
- [TwbNifBlock_ExtraDataByName](TwbNifBlock_ExtraDataByName.md)
- [TwbNifBlock_PropertyByType](TwbNifBlock_PropertyByType.md)
- [TwbNifBlock_AddExtraData](TwbNifBlock_AddExtraData.md)
