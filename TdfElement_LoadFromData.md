# TdfElement.LoadFromData

## Syntax

```pascal
procedure LoadFromData(const aData: TBytes);
```

Access via: `element.LoadFromData(Data)`

## Description

Loads binary data into this element by deserializing from a byte array.

The LoadFromData method populates this element with data from a byte array (TBytes). The binary data is parsed according to the element's definition structure, creating and populating all child elements as needed.

This is useful when you have binary data in memory (from a resource, network stream, or another source) and want to parse it into the structured element tree.

The element should be created from the appropriate definition before calling this method. Any existing data in the element is replaced.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aData | TBytes | The byte array containing binary data to deserialize |

## Returns

This method does not return a value.

## Example

```pascal
var
    nifFile: TwbNifFile;
    headerVersion: TdfElement;
    data: TBytes;
begin
    nifFile := TwbNifFile.Create;
    try
        nifFile.LoadFromData(data);
        headerVersion := nifFile.Elements['Header\Version'];
        if Assigned(headerVersion) then
            AddMessage('NIF Version: ' + headerVersion.EditValue);
    finally
        nifFile.Free;
    end;
end;
```

## See Also

- [TdfElement.LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement.LoadFromResource](TdfElement_LoadFromResource.md)
- [TdfElement.SaveToFile](TdfElement_SaveToFile.md)
- [TdfElement.DataSize](TdfElement_DataSize.md)
