# xEdit Scripting API Documentation

Comprehensive documentation for xEdit's JvInterpreter scripting system, covering plugin record manipulation, binary file format processing, and game asset management.

---

## 📚 Quick Navigation

| Section | Description | Functions |
|---------|-------------|-----------|
| [Plugin Records](#plugin-records) | Work with ESP/ESM/ESL files and game records | ~200 |
| [Binary Formats](#binary-formats) | NIF meshes, materials, LOD files, textures | ~100 |
| [Utility Functions](#utility-functions) | Math, strings, collections, grid cells | ~20 |
| [Resources](#resources) | Glossary, examples, tutorials | - |

**Total Documented Functions:** ~377 | **Coverage:** >90% of core API

---

## 🎮 Plugin Records

### Global Functions
_File management, messaging, and utilities_

**File Operations:**
- [FileCount](Global_FileCount.md) - Get total loaded files
- [FileByIndex](Global_FileByIndex.md) - Access file by index
- [FileByLoadOrder](Global_FileByLoadOrder.md) - Access file by load order
- [FileByName](Global_FileByName.md) - Access file by name
- [AddNewFile](Global_AddNewFile.md) - Create new plugin
- [AddNewFileName](Global_AddNewFileName.md) - Create plugin with name

**Messaging:**
- [AddMessage](Global_AddMessage.md) - Log message to console
- [ClearMessages](Global_ClearMessages.md) - Clear message log

**Utilities:**
- [GetRecordDefNames](Global_GetRecordDefNames.md) - Get all record type signatures
- [IntToHex64](Global_IntToHex64.md) - Convert Int64 to hex string
- [JumpTo](Global_JumpTo.md) - Navigate UI to element
- [ObjectToElement](Global_ObjectToElement.md) - Convert variant to IwbElement
- [FullPathToFileName](Global_FullPathToFileName.md) - Extract filename from path

**Plugin Flags:**
- [EnableSkyrimSaveFormat](Global_EnableSkyrimSaveFormat.md) - Enable Skyrim save format
- [wbIsPseudoESLMode](Global_wbIsPseudoESLMode.md) - Check ESL mode
- [wbIsPseudoLightMode](Global_wbIsPseudoLightMode.md) - Check light mode
- [wbIsPseudoMediumMode](Global_wbIsPseudoMediumMode.md) - Check medium mode
- [wbIsPseudoSmallMode](Global_wbIsPseudoSmallMode.md) - Check small mode

**String Processing:**
- [wbFilterStrings](Global_wbFilterStrings.md) - Filter string list by criteria
- [wbRemoveDuplicateStrings](Global_wbRemoveDuplicateStrings.md) - Remove duplicates

---

### IwbElement
_Base interface for all plugin data structures (records, fields, etc.)_

<details>
<summary><b>Core Operations (58 functions)</b> - Click to expand</summary>

**Identification:**
- [Name](IwbElement_Name.md) - Element name
- [BaseName](IwbElement_BaseName.md) - Element base name
- [ShortName](IwbElement_ShortName.md) - Abbreviated name
- [DisplayName](IwbElement_DisplayName.md) - UI display name
- [PathName](IwbElement_PathName.md) - Full path with names
- [Path](IwbElement_Path.md) - Indexed path
- [IndexedPath](IwbElement_IndexedPath.md) - Indexed path string
- [FullPath](IwbElement_FullPath.md) - Complete hierarchy path

**Type Information:**
- [ElementType](IwbElement_ElementType.md) - Element type enum
- [ElementTypeAsText](IwbElement_ElementTypeAsText.md) - Type as string
- [DefType](IwbElement_DefType.md) - Definition type enum
- [DefTypeAsText](IwbElement_DefTypeAsText.md) - Definition type as string

**Value Access:**
- [GetValue](IwbElement_GetValue.md) - Get value (display string)
- [GetEditValue](IwbElement_GetEditValue.md) - Get editable value
- [GetNativeValue](IwbElement_GetNativeValue.md) - Get native type value
- [SetEditValue](IwbElement_SetEditValue.md) - Set editable value
- [SetNativeValue](IwbElement_SetNativeValue.md) - Set native value
- [GetSummary](IwbElement_GetSummary.md) - Get summary string
- [SortKey](IwbElement_SortKey.md) - Get sort key

**Navigation:**
- [GetContainer](IwbElement_GetContainer.md) - Get parent container
- [GetFile](IwbElement_GetFile.md) - Get containing file
- [ContainingMainRecord](IwbElement_ContainingMainRecord.md) - Get parent record
- [LinksTo](IwbElement_LinksTo.md) - Get referenced element

**State Management:**
- [GetElementState](IwbElement_GetElementState.md) - Get element state flags
- [SetElementState](IwbElement_SetElementState.md) - Set element state flags
- [ClearElementState](IwbElement_ClearElementState.md) - Clear state flags
- [IsEditable](IwbElement_IsEditable.md) - Check if editable
- [IsInjected](IwbElement_IsInjected.md) - Check if injected
- [Assigned](IwbElement_Assigned.md) - Check if assigned (not nil)

**Modification:**
- [BeginUpdate](IwbElement_BeginUpdate.md) - Begin batch update
- [EndUpdate](IwbElement_EndUpdate.md) - End batch update
- [MarkModifiedRecursive](IwbElement_MarkModifiedRecursive.md) - Mark modified
- [SetToDefault](IwbElement_SetToDefault.md) - Reset to default value
- [Remove](IwbElement_Remove.md) - Remove element
- [ElementAssign](IwbElement_ElementAssign.md) - Copy from another element

**Movement:**
- [CanMoveUp](IwbElement_CanMoveUp.md) - Check if can move up
- [CanMoveDown](IwbElement_CanMoveDown.md) - Check if can move down
- [MoveUp](IwbElement_MoveUp.md) - Move element up
- [MoveDown](IwbElement_MoveDown.md) - Move element down

**Conflict Detection:**
- [ConflictAllForNode](IwbElement_ConflictAllForNode.md) - Check conflicts across overrides
- [ConflictThisForNode](IwbElement_ConflictThisForNode.md) - Check conflict for this override
- [OverrideCount](IwbElement_OverrideCount.md) - Get override count (deprecated)

**Validation:**
- [Check](IwbElement_Check.md) - Validate element
- [CanContainFormIDs](IwbElement_CanContainFormIDs.md) - Check if contains FormIDs
- [ReportRequiredMasters](IwbElement_ReportRequiredMasters.md) - Report required masters
- [BuildRef](IwbElement_BuildRef.md) - Build reference list

**Templates:**
- [AssignTemplateCount](IwbElement_AssignTemplateCount.md) - Get template count
- [AssignTemplateByIndex](IwbElement_AssignTemplateByIndex.md) - Get template by index
- [AssignTemplateByName](IwbElement_AssignTemplateByName.md) - Get template by name
- [TemplateAssign](IwbElement_TemplateAssign.md) - Assign from template

**Enum/Flag Helpers:**
- [EnumValues](IwbElement_EnumValues.md) - Get enum value list
- [FlagValues](IwbElement_FlagValues.md) - Get flag value list

**Utility:**
- [Equals](IwbElement_Equals.md) - Compare elements
- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md) - Copy to file
- [wbCopyElementToFileWithPrefix](IwbElement_wbCopyElementToFileWithPrefix.md) - Copy with prefix
- [wbCopyElementToFileWithPrefixAndSuffix](IwbElement_wbCopyElementToFileWithPrefixAndSuffix.md) - Copy with prefix/suffix
- [wbCopyElementToRecord](IwbElement_wbCopyElementToRecord.md) - Copy to record

</details>

---

### IwbContainer
_Interface for elements that contain child elements (records, structs, arrays)_

<details>
<summary><b>Container Operations (20 functions)</b> - Click to expand</summary>

**Access:**
- [ElementCount](IwbContainer_ElementCount.md) - Get child count
- [ElementByIndex](IwbContainer_ElementByIndex.md) - Get child by index
- [ElementByName](IwbContainer_ElementByName.md) - Get child by name
- [ElementByPath](IwbContainer_ElementByPath.md) - Get child by path
- [ElementBySignature](IwbContainer_ElementBySignature.md) - Get child by signature
- [ElementExists](IwbContainer_ElementExists.md) - Check if child exists
- [LastElement](IwbContainer_LastElement.md) - Get last child
- [AdditionalElementCount](IwbContainer_AdditionalElementCount.md) - Get additional element count

**Modification:**
- [Add](IwbContainer_Add.md) - Add new element
- [AddElement](IwbContainer_AddElement.md) - Add element with type
- [InsertElement](IwbContainer_InsertElement.md) - Insert element at position
- [RemoveElement](IwbContainer_RemoveElement.md) - Remove child element
- [RemoveByIndex](IwbContainer_RemoveByIndex.md) - Remove by index
- [ReverseElements](IwbContainer_ReverseElements.md) - Reverse child order
- [IndexOf](IwbContainer_IndexOf.md) - Get child index

**Batch Operations:**
- [GetElementValues](IwbContainer_GetElementValues.md) - Get all child values
- [GetElementEditValues](IwbContainer_GetElementEditValues.md) - Get all edit values
- [GetElementNativeValues](IwbContainer_GetElementNativeValues.md) - Get all native values
- [SetElementEditValues](IwbContainer_SetElementEditValues.md) - Set all edit values
- [SetElementNativeValues](IwbContainer_SetElementNativeValues.md) - Set all native values

**State:**
- [ContainerStates](IwbContainer_ContainerStates.md) - Get container state flags
- [IsSorted](IwbContainer_IsSorted.md) - Check if sorted

</details>

---

### IwbFile
_Interface for ESP/ESM/ESL plugin files_

<details>
<summary><b>File Operations (36 functions)</b> - Click to expand</summary>

**File Properties:**
- [GetFileName](IwbFile_GetFileName.md) - Get filename
- [GetLoadOrder](IwbFile_GetLoadOrder.md) - Get load order index
- [GetLoadOrderFileID](IwbFile_GetLoadOrderFileID.md) - Get load order file ID

**File Flags:**
- [GetIsESM](IwbFile_GetIsESM.md) / [SetIsESM](IwbFile_SetIsESM.md) - Master flag
- [GetIsESL](IwbFile_GetIsESL.md) / [SetIsESL](IwbFile_SetIsESL.md) - ESL flag
- [GetIsLight](IwbFile_GetIsLight.md) / [SetIsLight](IwbFile_SetIsLight.md) - Light flag (SSE)
- [GetIsMedium](IwbFile_GetIsMedium.md) / [SetIsMedium](IwbFile_SetIsMedium.md) - Medium flag
- [GetIsSmall](IwbFile_GetIsSmall.md) / [SetIsSmall](IwbFile_SetIsSmall.md) - Small flag
- [CanBeESL](IwbFile_CanBeESL.md) - Check if can be ESL
- [CanBeLight](IwbFile_CanBeLight.md) - Check if can be light
- [CanBeMedium](IwbFile_CanBeMedium.md) - Check if can be medium
- [CanBeSmall](IwbFile_CanBeSmall.md) - Check if can be small

**Masters:**
- [MasterCount](IwbFile_MasterCount.md) - Get master count
- [MasterByIndex](IwbFile_MasterByIndex.md) - Get master by index
- [GetMasters](IwbFile_GetMasters.md) - Get all masters
- [HasMaster](IwbFile_HasMaster.md) - Check if has master
- [AddMasters](IwbFile_AddMasters.md) - Add multiple masters
- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md) - Add single master
- [AddMastersIfMissing](IwbFile_AddMastersIfMissing.md) - Add multiple if missing
- [CleanMasters](IwbFile_CleanMasters.md) - Remove unused masters
- [SortMasters](IwbFile_SortMasters.md) - Sort master list

**Records:**
- [RecordCount](IwbFile_RecordCount.md) - Get record count
- [RecordByIndex](IwbFile_RecordByIndex.md) - Get record by index
- [RecordByFormID](IwbFile_RecordByFormID.md) - Find record by FormID
- [RecordByEditorID](IwbFile_RecordByEditorID.md) - Find record by EditorID
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md) - Get record from this file

**Groups:**
- [GroupBySignature](IwbFile_GroupBySignature.md) - Get group by signature
- [HasGroup](IwbFile_HasGroup.md) - Check if has group

**FormID Conversion:**
- [GetNewFormID](IwbFile_GetNewFormID.md) - Get next available FormID
- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md) - File → Load order
- [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md) - Load order → File

**Serialization:**
- [FileWriteToStream](IwbFile_FileWriteToStream.md) - Write file to stream

</details>

---

### IwbMainRecord
_Interface for game records (NPCs, weapons, cells, etc.)_

<details>
<summary><b>Record Operations (48 functions)</b> - Click to expand</summary>

**Identification:**
- [Signature](IwbMainRecord_Signature.md) - 4-char record type (WEAP, NPC_, etc.)
- [FormID](IwbMainRecord_FormID.md) - File-local FormID
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md) / [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md) - Load order FormID
- [FixedFormID](IwbMainRecord_FixedFormID.md) - Fixed FormID (ESL)
- [EditorID](IwbMainRecord_EditorID.md) / [SetEditorID](IwbMainRecord_SetEditorID.md) - Editor ID

**Flags:**
- [GetIsDeleted](IwbMainRecord_GetIsDeleted.md) / [SetIsDeleted](IwbMainRecord_SetIsDeleted.md) - Deleted flag
- [GetIsPersistent](IwbMainRecord_GetIsPersistent.md) / [SetIsPersistent](IwbMainRecord_SetIsPersistent.md) - Persistent flag
- [GetIsInitiallyDisabled](IwbMainRecord_GetIsInitiallyDisabled.md) / [SetIsInitiallyDisabled](IwbMainRecord_SetIsInitiallyDisabled.md) - Disabled flag
- [GetIsVisibleWhenDistant](IwbMainRecord_GetIsVisibleWhenDistant.md) / [SetIsVisibleWhenDistant](IwbMainRecord_SetIsVisibleWhenDistant.md) - VWD flag

**Versioning:**
- [GetFormVersion](IwbMainRecord_GetFormVersion.md) / [SetFormVersion](IwbMainRecord_SetFormVersion.md) - Form version
- [GetFormVCS1](IwbMainRecord_GetFormVCS1.md) / [SetFormVCS1](IwbMainRecord_SetFormVCS1.md) - Version control 1
- [GetFormVCS2](IwbMainRecord_GetFormVCS2.md) / [SetFormVCS2](IwbMainRecord_SetFormVCS2.md) - Version control 2

**Overrides:**
- [IsMaster](IwbMainRecord_IsMaster.md) - Check if master record
- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md) - Check if winning override
- [Master](IwbMainRecord_Master.md) - Get master record
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md) - Get master or self
- [WinningOverride](IwbMainRecord_WinningOverride.md) - Get winning override
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md) - Get highest override
- [OverrideCount](IwbMainRecord_OverrideCount.md) - Get override count
- [OverrideByIndex](IwbMainRecord_OverrideByIndex.md) - Get override by index

**References:**
- [ReferencesCount](IwbMainRecord_ReferencesCount.md) - Count outgoing references
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md) - Get outgoing reference
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md) - Count incoming references
- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md) - Get incoming reference
- [UpdateRefs](IwbMainRecord_UpdateRefs.md) - Update reference caches

**Children:**
- [ChildGroup](IwbMainRecord_ChildGroup.md) - Get child group

**Conflict Detection:**
- [ConflictAllForMainRecord](IwbMainRecord_ConflictAllForMainRecord.md) - Conflict across all
- [ConflictThisForMainRecord](IwbMainRecord_ConflictThisForMainRecord.md) - Conflict for this

**Spatial (References):**
- [GetGridCell](IwbMainRecord_GetGridCell.md) - Get grid cell coordinates
- [GetPosition](IwbMainRecord_GetPosition.md) - Get position (x, y, z)
- [GetRotation](IwbMainRecord_GetRotation.md) - Get rotation (x, y, z)

**Precombined Meshes (FO4):**
- [HasPrecombinedMesh](IwbMainRecord_HasPrecombinedMesh.md) - Check if has precombined mesh
- [PrecombinedMesh](IwbMainRecord_PrecombinedMesh.md) - Get precombined mesh data

**Utilities:**
- [BaseRecord](IwbMainRecord_BaseRecord.md) - Get base record
- [BaseRecordID](IwbMainRecord_BaseRecordID.md) - Get base record FormID
- [ChangeFormSignature](IwbMainRecord_ChangeFormSignature.md) - Change record type
- [CompareExchangeFormID](IwbMainRecord_CompareExchangeFormID.md) - Atomic FormID update

</details>

---

### IwbGroupRecord
_Interface for record groups (GRUP records)_

- [GroupLabel](IwbGroupRecord_GroupLabel.md) - Get group label (signature or FormID)
- [GroupType](IwbGroupRecord_GroupType.md) - Get group type (0-10)
- [ChildrenOf](IwbGroupRecord_ChildrenOf.md) - Get parent record for child groups
- [FindChildGroup](IwbGroupRecord_FindChildGroup.md) - Find child group by type
- [MainRecordByEditorID](IwbGroupRecord_MainRecordByEditorID.md) - Find record in group

---

### IwbResource
_Interface for BSA/BA2 archive access_

- [ResourceContainerList](IwbResource_ResourceContainerList.md) - Get all resource containers
- [ResourceCount](IwbResource_ResourceCount.md) - Count resources in folder
- [ResourceList](IwbResource_ResourceList.md) - List resources in folder
- [ResourceExists](IwbResource_ResourceExists.md) - Check if resource exists
- [ResourceOpenData](IwbResource_ResourceOpenData.md) - Read resource data
- [ResourceCopy](IwbResource_ResourceCopy.md) - Extract resource to disk

---

## 🎨 Binary Formats

### Global Functions
_Data format utilities_

- [dfFloatToStr](Global_dfFloatToStr.md) - Convert float to string (DF format)
- [dfStrToFloat](Global_dfStrToFloat.md) - Parse string to float (DF format)
- [dfCalcHash](Global_dfCalcHash.md) - Calculate hash for binary data

---

### File Format Classes
_Binary file format constructors (NIF, materials, LOD, textures)_

**Materials:**
- [TwbBGSMFile.Create](TwbBGSMFile_Create.md) - Bethesda Material (FO4/FO76)
- [TwbBGEMFile.Create](TwbBGEMFile_Create.md) - Bethesda Effect Material (particles)

**LOD Files:**
- [TwbLODTreeLSTFile.Create](TwbLODTreeLSTFile_Create.md) - Tree LOD list
- [TwbLODTreeBTTFile.Create](TwbLODTreeBTTFile_Create.md) - Billboard tree texture atlas
- [TwbLODSettingsFO3File.Create](TwbLODSettingsFO3File_Create.md) - FO3/FNV LOD settings
- [TwbLODSettingsTES5File.Create](TwbLODSettingsTES5File_Create.md) - Skyrim/FO4 LOD settings

**Other Formats:**
- [TwbFUZFile.Create](TwbFUZFile_Create.md) - Facial animation + audio (FUZ)
- [TwbDDSFile.Create](TwbDDSFile_Create.md) - DirectDraw Surface textures (DDS)

---

### TdfDef
_Binary format schema/definition (equivalent to IwbDef for plugin records)_

- [Name](TdfDef_Name.md) - Definition name
- [DefaultDataSize](TdfDef_DefaultDataSize.md) - Default binary size in bytes
- [DefaultValue](TdfDef_DefaultValue.md) - Default initialization value
- [Size](TdfDef_Size.md) - Fixed size constraint

---

### TdfElement
_Binary file format element (equivalent to IwbElement for plugin records)_

<details>
<summary><b>TdfElement Operations (37 functions)</b> - Click to expand</summary>

**Identity:**
- [DataType](TdfElement_DataType.md) - Data type enum
- [Def](TdfElement_Def.md) - Get definition (TdfDef)
- [Name](TdfElement_Name.md) - Element name
- [Path](TdfElement_Path.md) - Full path string
- [Root](TdfElement_Root.md) - Get root element
- [Parent](TdfElement_Parent.md) - Get parent element
- [Index](TdfElement_Index.md) - Index in parent

**Structure:**
- [Count](TdfElement_Count.md) - Child count
- [DataSize](TdfElement_DataSize.md) - Binary size in bytes
- [Enabled](TdfElement_Enabled.md) - Get/set enabled state

**Values:**
- [NativeValue](TdfElement_NativeValue.md) - Binary value
- [EditValue](TdfElement_EditValue.md) - Human-readable value
- [NativeValues](TdfElement_NativeValues.md) - Indexed binary values
- [EditValues](TdfElement_EditValues.md) - Indexed edit values
- [Items](TdfElement_Items.md) - Indexed items (variant)
- [Elements](TdfElement_Elements.md) - Indexed elements (TdfElement)

**Batch Updates:**
- [BeginUpdate](TdfElement_BeginUpdate.md) - Begin batch update
- [EndUpdate](TdfElement_EndUpdate.md) - End batch update

**Navigation:**
- [ElementByName](TdfElement_ElementByName.md) - Find child by name
- [ElementByPath](TdfElement_ElementByPath.md) - Find child by path
- [IndexOf](TdfElement_IndexOf.md) - Get child index

**Modification:**
- [Add](TdfElement_Add.md) - Add child element
- [Remove](TdfElement_Remove.md) - Remove child element
- [Delete](TdfElement_Delete.md) - Delete child by index
- [Move](TdfElement_Move.md) - Move child element
- [SetToDefault](TdfElement_SetToDefault.md) - Reset to default
- [Assign](TdfElement_Assign.md) - Copy from another element

**I/O:**
- [LoadFromData](TdfElement_LoadFromData.md) - Load from byte array
- [LoadFromFile](TdfElement_LoadFromFile.md) - Load from file
- [LoadFromJSONFile](TdfElement_LoadFromJSONFile.md) - Load from JSON
- [LoadFromResource](TdfElement_LoadFromResource.md) - Load from BSA
- [SaveToFile](TdfElement_SaveToFile.md) - Save to file
- [SaveToJSONFile](TdfElement_SaveToJSONFile.md) - Save to JSON

**Serialization:**
- [FromJSON](TdfElement_FromJSON.md) - Import from JSON
- [ToJSON](TdfElement_ToJSON.md) - Export to JSON
- [ToText](TdfElement_ToText.md) - Convert to text

**References:**
- [LinksTo](TdfElement_LinksTo.md) - Get referenced element

</details>

---

### NIF Files (NetImmerse/Gamebryo Meshes)

#### TwbNiRef
_NIF block reference/pointer_

- [Template](TwbNiRef_Template.md) - Expected block type template
- [Ptr](TwbNiRef_Ptr.md) - Reference direction (forward/backward)

---

#### TwbNifBlock
_NIF block (scene graph node, geometry, property, etc.)_

<details>
<summary><b>TwbNifBlock Operations (20 functions)</b> - Click to expand</summary>

**Properties:**
- [BlockType](TwbNifBlock_BlockType.md) - Block type name (NiTriShape, NiNode, etc.)
- [NifFile](TwbNifBlock_NifFile.md) - Get parent NIF file
- [RefsCount](TwbNifBlock_RefsCount.md) - Get reference count
- [Refs](TwbNifBlock_Refs.md) - Get reference by index
- [StringsCount](TwbNifBlock_StringsCount.md) - Get string count
- [Strings](TwbNifBlock_Strings.md) - Get string by index

**Type Testing:**
- [IsNiObject](TwbNifBlock_IsNiObject.md) - Check block type (supports inheritance)

**Scene Graph:**
- [AddChild](TwbNifBlock_AddChild.md) - Add child block
- [ChildByType](TwbNifBlock_ChildByType.md) - Find first child by type
- [ChildrenByType](TwbNifBlock_ChildrenByType.md) - Find all children by type

**Properties:**
- [AddProperty](TwbNifBlock_AddProperty.md) - Add property block
- [PropertyByName](TwbNifBlock_PropertyByName.md) - Find property by name
- [PropertyByType](TwbNifBlock_PropertyByType.md) - Find first property by type
- [PropertiesByType](TwbNifBlock_PropertiesByType.md) - Find all properties by type

**Extra Data:**
- [AddExtraData](TwbNifBlock_AddExtraData.md) - Add extra data block
- [ExtraDataByName](TwbNifBlock_ExtraDataByName.md) - Find extra data by name
- [ExtraDataByType](TwbNifBlock_ExtraDataByType.md) - Find first extra data by type
- [ExtraDatasByType](TwbNifBlock_ExtraDatasByType.md) - Find all extra data by type

**Geometry:**
- [UpdateBounds](TwbNifBlock_UpdateBounds.md) - Recalculate bounding box
- [UpdateNormals](TwbNifBlock_UpdateNormals.md) - Recalculate vertex normals
- [UpdateTangents](TwbNifBlock_UpdateTangents.md) - Recalculate tangent space

**Assets:**
- [GetAssetsList](TwbNifBlock_GetAssetsList.md) - Get referenced asset paths

</details>

---

#### TwbNifFile
_NIF file (3D mesh container)_

<details>
<summary><b>TwbNifFile Operations (24 functions)</b> - Click to expand</summary>

**Constructor:**
- [Create](TwbNifFile_Create.md) - Create NIF file handler

**Version:**
- [NifVersion](TwbNifFile_NifVersion.md) - Get/set NIF version (1-6: MW, OB, FO3, TES5, SSE, FO4)

**Processing:**
- [InternalUpdates](TwbNifFile_InternalUpdates.md) - Get/set internal update mode
- [Options](TwbNifFile_Options.md) - Get/set processing options

**Structure:**
- [Header](TwbNifFile_Header.md) - Get header block
- [Footer](TwbNifFile_Footer.md) - Get footer block
- [BlocksCount](TwbNifFile_BlocksCount.md) - Get block count
- [Blocks](TwbNifFile_Blocks.md) - Get block by index

**Block Management:**
- [AddBlock](TwbNifFile_AddBlock.md) - Add new block
- [InsertBlock](TwbNifFile_InsertBlock.md) - Insert block at position
- [ConvertBlock](TwbNifFile_ConvertBlock.md) - Convert block to another type
- [CopyBlock](TwbNifFile_CopyBlock.md) - Copy block from another NIF

**Block Search:**
- [BlockByType](TwbNifFile_BlockByType.md) - Find first block by type
- [BlocksByType](TwbNifFile_BlocksByType.md) - Find all blocks by type
- [BlockByName](TwbNifFile_BlockByName.md) - Find block by name

**Batch Operations (Spells):**
- [SpellTriangulate](TwbNifFile_SpellTriangulate.md) - Convert triangle strips to triangles
- [SpellFaceNormals](TwbNifFile_SpellFaceNormals.md) - Recalculate all normals
- [SpellUpdateTangents](TwbNifFile_SpellUpdateTangents.md) - Update existing tangents
- [SpellAddUpdateTangents](TwbNifFile_SpellAddUpdateTangents.md) - Add/update tangents

**Assets:**
- [GetAssetsList](TwbNifFile_GetAssetsList.md) - Get all referenced assets

</details>

---

## 🧰 Utility Functions

### Math
_Mathematical operations_

- [Lerp](Math_Lerp.md) - Linear interpolation (clamped)
- [LerpUnclamped](Math_LerpUnclamped.md) - Linear interpolation (unclamped)
- [InverseLerp](Math_InverseLerp.md) - Inverse linear interpolation
- [InRange](Math_InRange.md) - Check if value in range
- [IfThen](Math_IfThen.md) - Conditional value selection

---

### StrUtils
_String utilities_

- [IfThen](StrUtils_IfThen.md) - Conditional string selection

---

### TStringList
_String collection operations_

- [CaseSensitive](TStringList_CaseSensitive.md) - Get/set case sensitivity
- [Union](TStringList_Union.md) - Set union
- [Intersection](TStringList_Intersection.md) - Set intersection
- [Difference](TStringList_Difference.md) - Set difference
- [SymmetricDifference](TStringList_SymmetricDifference.md) - Set symmetric difference

---

### TwbGridCell
_Worldspace grid cell coordinates (4096-unit squares)_

- [wbPositionToGridCell](TwbGridCell_wbPositionToGridCell.md) - Convert position to grid cell
- [wbIsInGridCell](TwbGridCell_wbIsInGridCell.md) - Test if position in grid cell
- [wbGridCellToGroupLabel](TwbGridCell_wbGridCellToGroupLabel.md) - Convert to group label
- [wbSubBlockFromGridCell](TwbGridCell_wbSubBlockFromGridCell.md) - Convert to sub-block
- [wbBlockFromSubBlock](TwbGridCell_wbBlockFromSubBlock.md) - Convert to parent block

---

## 📖 Resources

### Documentation
- [Glossary](Glossary.md) - Technical terms and concepts
- [Constants](Constants.md) - Enumerations and constants

### Development
- [TODO](TODO.md) - Planned improvements and missing documentation

---

## 📊 Documentation Stats

- **Total Functions:** ~377
- **Plugin Record API:** ~200 functions (IwbElement, IwbContainer, IwbFile, IwbMainRecord, etc.)
- **Binary Format API:** ~100 functions (TdfElement, TwbNifFile, file formats)
- **Utility Functions:** ~20 functions (Math, StrUtils, TStringList, TwbGridCell)
- **Coverage:** >90% of core xEdit scripting API

---

## 🎯 Getting Started

**Common Tasks:**

1. **Load a plugin and read records:**
   ```pascal
   var
     f: IwbFile;
     i: Integer;
     rec: IwbMainRecord;
   begin
     f := FileByName('MyPlugin.esp');
     for i := 0 to Pred(RecordCount(f)) do begin
       rec := RecordByIndex(f, i);
       AddMessage(EditorID(rec));
     end;
   end;
   ```

2. **Load and modify a NIF file:**
   ```pascal
   var
     nif: TwbNifFile;
     block: TwbNifBlock;
   begin
     nif := TwbNifFile.Create;
     nif.LoadFromFile('meshes\armor\sword.nif');
     nif.UpdateNormals;
     nif.UpdateTangents;
     nif.SaveToFile('meshes\armor\sword_fixed.nif');
   end;
   ```

3. **Work with materials:**
   ```pascal
   var
     mat: TdfElement;
   begin
     mat := TwbBGSMFile.Create;
     mat.LoadFromFile('materials\metal\steel.bgsm');
     mat.EditValues['Diffuse Texture'] := 'textures\custom\diffuse.dds';
     mat.SaveToFile('materials\metal\steel_custom.bgsm');
   end;
   ```

---

**Questions?** See the [Glossary](Glossary.md) for technical terms.
