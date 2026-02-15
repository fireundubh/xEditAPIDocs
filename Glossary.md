# Glossary

## B

### Base Record

The original [record](#record) definition that a [reference](#reference) points to. For example, a `REFR` (placed object reference) links to a base record like `WEAP` (weapon), `NPC_` (character), or `ARMO` (armor) that defines the object's properties. The base record contains the template data, while references represent individual instances of that object placed in the game world.

### BGEM

Bethesda Effect Material - a binary material file format introduced in Fallout 4 and used in Fallout 76 and Starfield. BGEM files define effect materials such as particle effects, glowing materials, and other shader-based visual effects. Works alongside [BGSM](#bgsm) files to provide complete material definitions for game assets.

### BGSM

Bethesda Material - a binary material file format introduced in Fallout 4 and used in Fallout 76 and Starfield. BGSM files define material properties for 3D models including texture paths, shader parameters, opacity, specularity, and other rendering properties. Replaces the older NIF-embedded material system used in earlier games.

### BSA

Bethesda Archive - a proprietary compressed archive format used by Bethesda Game Studios to package game assets (textures, models, sounds, etc.) for their games.

## C

### Cell

A container for game world data representing either an interior space (interior cell) or a section of an exterior space (exterior cell). Cells contain [references](#reference) (placed objects), lighting, encounter zones, and other environmental data. Exterior cells are organized within a [worldspace](#worldspace) using a grid system, while interior cells exist independently. See also: [Exterior Cell](#exterior-cell), [Interior Cell](#interior-cell).

### Child Group

A subgroup of [records](#record) that belong to a parent record. Most commonly seen in worldspaces and cells, where the child group contains [references](#reference) (placed objects) for that location. Child groups organize hierarchical data structures within plugins.

### Creation Engine

Bethesda's proprietary game engine used for The Elder Scrolls V: Skyrim (2011), Fallout 4 (2015), Fallout 76 (2018), and Starfield (2023). Evolution of the [Gamebryo](#gamebryo) engine with enhanced graphics, physics, and scripting capabilities. Uses [NIF](#nif) files for 3D models and introduces [BGSM](#bgsm)/[BGEM](#bgem) material formats in later iterations.

### Creation Kit

Bethesda's official modding tool for [Creation Engine](#creation-engine) games. Provides a graphical interface for editing plugins, creating quests, building interiors, placing objects, and scripting game logic. Different versions exist for each game (Skyrim Creation Kit, Fallout 4 Creation Kit, etc.). Often generates [Identical to Master](#identical-to-master-record) records that require cleaning with xEdit.

### Container

Any [element](#element) that contains or can contain other elements

### CRC32

Cyclic Redundancy Check 32-bit - a hash function that produces a 32-bit checksum value used to detect accidental changes to raw data. Commonly used for verifying file integrity and resource archives.

## D

### DDS

DirectDraw Surface - a Microsoft image file format used for storing textures and environment maps. Widely used in video games for efficient GPU texture storage and supports various compression formats.

### DLSTRINGS

Dialog Localized Strings - a binary file format (`.DLSTRINGS`) used by Skyrim and later games to store externalized dialogue text in multiple languages. Part of the [localization](#localization) system alongside [STRINGS](#strings) and [ILSTRINGS](#ilstrings) files. DLSTRINGS specifically contains dialogue text that can vary in length.

## E

### Editor ID

A human-readable string identifier not used by any game and intended for organizational purposes. However, [records](#record) whose [signature](#signature) is `GMST` are *uniquely* identified by Editor ID and will be overridden by later loading `GMST` records with matching Editor IDs.

### Element

All objects in xEdit are elements. There are two element archetypes:

- An element with a [signature](#signature) exists as data in the plugin itself. Also called a [subrecord](#subrecord).
- An element without a signature exists only in xEdit to represent the logical structure of parsed plugin data. These elements are not found in or saved to plugins.

### ESL

Elder Scrolls Light - a [plugin](#plugin) file format (`.esl`) introduced in Fallout 4 and used in subsequent games. ESL plugins use a compact [Form ID](#form-id) format (FExxxyyy) that allows thousands of light plugins to load simultaneously without consuming limited plugin slots. ESL files have restrictions: they can only contain up to 2,048 new records with unique Form IDs, but can include unlimited [overriding records](#overriding-record).

### ESM

Elder Scrolls Master - a [plugin](#plugin) file format (`.esm`) that serves as a [master file](#master-file) for other plugins. ESM files load before ESP files in the load order and use a 2-character [Mod ID](#mod-id) in their [Form ID](#form-id) format (xxyyyyyy). Typically used for game data files and major expansion packs.

### ESP

Elder Scrolls Plugin - the standard [plugin](#plugin) file format (`.esp`) for mods. ESP files load after [ESM](#esm) files in the load order and use the same [Form ID](#form-id) format (xxyyyyyy) with a 2-character [Mod ID](#mod-id). Most user-created mods use the ESP format.

### Exterior Cell

A [cell](#cell) that represents outdoor game space within a [worldspace](#worldspace). Exterior cells are organized in a grid system using [grid cell](#grid-cell) coordinates. Multiple exterior cells can be loaded simultaneously to create seamless outdoor environments. Contrast with [Interior Cell](#interior-cell).

## F

### File Form ID

A [Form ID](#form-id) where the [Mod ID](#mod-id) is relative to the plugin's [master files](#master-file)

For example, `Dragonborn.esm` has the master files `[Skyrim.esm, Update.esm]`.

In that 0-based array:

- `Skyrim.esm` is at index 0,
- `Update.esm` at index 1, and
- the next available index would be 2, which is the local Mod ID for `Dragonborn.esm`.

### Form ID

An 8-character hexadecimal identifier whose format varies with the containing plugin's file type

The Form ID format for ESP and ESM records has two parts:

1. a 2-character [Mod ID](#mod-id), and
2. a 6-character [Object ID](#object-id) (e.g., `xxyyyyyy`.)

The Form ID format for ESL records has three parts:

1. an `FE` prefix,
2. a 3-character [Light Mod ID](#light-mod-id), and
3. a 3-character Object ID (e.g., `FExxxyyy`.)

### Form Version

A value stored in the [record header](#record-header) that tracks the format version of a [record](#record). Form versions allow games to update record structures across patches while maintaining backward compatibility. For example, Fallout 4 records may have form version 40 (base game) or 44 (version 1.10+). Different form versions can have different data layouts for the same [signature](#signature).

### FUZ

Facial Animation + Audio - Bethesda's container file format (`.fuz`) that combines lip-sync facial animation data with compressed audio ([XWM](#xwm) format). Used extensively in Skyrim and Fallout games for NPC dialogue, packaging spoken audio together with phoneme timing data for realistic lip synchronization during conversations.

## G

### Group Record

A container [record](#record) that organizes and groups [main records](#main-record) of the same type or belonging to the same parent. Group records use the `GRUP` signature and can be organized by record type (e.g., all `WEAP` records), by parent (e.g., all [references](#reference) in a [cell](#cell)), or by [grid cell](#grid-cell). Group records are structural elements that don't have [Form IDs](#form-id) but are essential for organizing plugin data efficiently.

### Gamebryo

A commercial game engine developed by Gamebase Co., Ltd. and Emergent Game Technologies, used by Bethesda for The Elder Scrolls IV: Oblivion (2006), Fallout 3 (2008), and Fallout: New Vegas (2010). Predecessor to the [Creation Engine](#creation-engine). Uses [NIF](#nif) files for 3D models.

### Grid Cell

A coordinate unit in the game's worldspace system. Grid cells divide the world into manageable chunks, typically 4096 units square. Used for organizing exterior cell data and optimizing loading/rendering.

## H

### Hash

A cryptographic or non-cryptographic function that maps data of arbitrary size to fixed-size values. Common hash functions include CRC32, MD5, and SHA1, used for file integrity verification, resource identification, and data deduplication.

### Hardcoded Form

A [record](#record) whose [Object ID](#object-id) is less than or equal to `0x800` and exists only in the game's executable. In *Fallout 4* plugins, Object IDs can start at `0x1`, but in plugins for other games, Object IDs must always be greater than `0x800`. These rules are strictly enforced.

### HITME

An acronym for "**Hi**gher **T**han **M**asterlist **E**ntries," coined by [LOOT](https://loot.github.io) developer WrinklyNinja. When an [element](#element) links to a [record](#record) in a [master file](#master-file) that was improperly removed, that issue is called a **HITME**.

Broken links display as `< Error: Could not be resolved >`, although not all such errors are HITME issues.

## I

### Identical to Master Record

An [overriding record](#overriding-record) that does not change its [master record](#master-record) in any way. Some mod authors exploit Identical to Master (ITM) records to revert changes made by other plugins, or the Creation Kit may populate plugins with ITMs for no apparent reason. Most mod authors and players agree ITMs are problematic, if not harmful, and so xEdit is popularly used to "clean" ITMs from plugins.

### ILSTRINGS

Info Localized Strings - a binary file format (`.ILSTRINGS`) used by Skyrim and later games to store externalized info text (typically UI elements, book contents, and item descriptions) in multiple languages. Part of the [localization](#localization) system alongside [STRINGS](#strings) and [DLSTRINGS](#dlstrings) files.

### Initially Disabled

A flag on [reference](#reference) records (REFR, ACHR, etc.) that marks the placed object as disabled when the game starts. Initially disabled references can be enabled later through scripts or quest stages. Commonly used for quest-specific objects that should only appear at certain times.

### Injected Record

A record whose [Load Order Form ID](#load-order-form-id) is unreserved but treated as contained by the file matching the specified [Mod ID](#mod-id) or [Light Mod ID](#light-mod-id).

When injected records with different [signatures](#signature) conflict, the game will crash.

### Interior Cell

A [cell](#cell) that represents indoor game space, such as buildings, caves, or dungeons. Interior cells exist independently from worldspaces and load as isolated environments. Only one interior cell is typically loaded at a time. Contrast with [Exterior Cell](#exterior-cell).

## L

### Localization

The system for storing and retrieving translated game strings in language-specific files ([STRINGS](#strings), [DLSTRINGS](#dlstrings), [ILSTRINGS](#ilstrings)). Introduced in Skyrim, allows games to support multiple languages by externalizing text content from plugin files into separate binary string files for each language.

### LOD

Level of Detail - simplified versions of 3D models and textures used at greater distances to improve rendering performance. LOD generation creates these optimized assets automatically from full-detail game data.

### Light Mod ID

A 3-character hexadecimal identifier for an ESL file associated with the [Object ID](#object-id) in a [Form ID](#form-id). The term "light" comes from nomenclature used to distinguish between slots into which plugins are loaded. ESL plugins are loaded into "light slots" and other plugins into "full slots."

### Load Order

The sequence in which [plugins](#plugin) are loaded by the game. Load order determines which [overriding records](#overriding-record) take precedence through the [winning override](#winning-override) system. Later-loading plugins override earlier ones. The load order affects [Load Order Form IDs](#load-order-form-id) and is critical for mod compatibility. [ESM](#esm) files load before [ESP](#esp) files, and [ESL](#esl) files can load in light slots without consuming regular plugin slots.

### Load Order Form ID

A [Form ID](#form-id) where the [Mod ID](#mod-id) is relative to the current load order. Also called **Global Form ID** or **Save Game Form ID** depending on context.

For example, consider a load order containing these plugins:

```
[00] Skyrim.esm
[01] Update.esm
[02] Dawnguard.esm
[03] Dragonborn.esm
```

If `Dragonborn.esm` was reordered before `Dawnguard.esm`, the global Mod ID for `Dragonborn.esm` would change to `02`.

## M

### Main Record

A primary data [record](#record) in a [plugin](#plugin) that represents a game object, such as a weapon (`WEAP`), character (`NPC_`), quest (`QUST`), or placed object ([Reference](#reference)). Main records have [Form IDs](#form-id), can be overridden by other plugins, and are organized within [group records](#group-record). Contrast with [subrecords](#subrecord), which are data fields within main records.

### MD5

Message-Digest Algorithm 5 - a widely-used cryptographic hash function that produces a 128-bit hash value. While no longer considered secure for cryptographic purposes, it remains useful for file integrity verification and resource comparison.

### Master File

A [plugin](#plugin) on which another plugin depends. For a [record](#record) in a plugin to link to records outside its scope, that plugin must declare the source master files in its File Header. A plugin's master files has implications for its records' [File Form IDs](#file-form-id) and its load order.

### Master Record

A [record](#record) at the start of an [overriding record](#overriding-record) chain

### Mod ID

A 2-character hexadecimal identifier for an ESM or ESP plugin associated with the [Object ID](#object-id) in a [Form ID](#form-id)

## N

### Navigation Mesh

Also known as **Navmesh** - a 3D mesh that defines walkable surfaces and pathfinding data for NPCs and creatures. Navigation meshes enable AI-controlled characters to navigate the game world intelligently, avoiding obstacles and finding optimal paths to their destinations. Created and edited in the [Creation Kit](#creation-kit).

### NetImmerse

A game engine developed by Numerical Design Limited (NDL), used by Bethesda for The Elder Scrolls III: Morrowind (2002). The [NIF](#nif) file format is named after this engine (NetImmerse Format). Predecessor to [Gamebryo](#gamebryo).

### NIF

NetImmerse Format - the 3D model file format used by Gamebryo and Creation Engine games. NIF files contain mesh geometry, textures, animations, and other 3D asset data.

## O

### Object ID

A 3- or 6-character hexadecimal identifier for a [record](#record). The identifier will be the last three characters of a [Form ID](#form-id) in an ESL plugin, and the last six characters of a Form ID in ESM and ESP plugins.

### Override

To create a [record](#record) whose [Load Order Form ID](#load-order-form-id) is identical to a [master record](#master-record) in a different plugin for the purpose of modifying some or all aspects of that record. If no changes are made to the overriding record, that record becomes an [Identical to Master](#identical-to-master-record) issue.

### Overriding Record

A [record](#record) whose [Load Order Form ID](#load-order-form-id) matches that of a record in a different plugin. To override a record in a [plugin](#plugin), the record's parent file must be a [master files](#master-file) for the overriding record's parent file, except if the [signature](#signature) is `GMST` in which case only the Editor ID must match.

## P

### Persistent

A flag on [reference](#reference) records (REFR, ACHR, etc.) that keeps the placed object loaded in memory at all times, even when its [cell](#cell) is not active. Persistent references remain accessible to scripts from anywhere in the game world. Essential for objects that need to be referenced by scripts or quests regardless of the player's location.

### Precombined Mesh

A Fallout 4 optimization feature that merges multiple static mesh references into a single combined mesh to improve rendering performance. Precombined meshes reduce draw calls and improve frame rates in dense urban environments. Modifying or deleting references that are part of precombined meshes can cause visual glitches unless the precombined data is regenerated.

### Previs

Short for **Precomputed Visibility** - optimization data in Fallout 4 that determines which objects are visible from specific locations. Works alongside [precombined meshes](#precombined-mesh) to improve performance by culling objects that cannot be seen from the player's current position. Like precombined meshes, modifying worldspace data may require regenerating previs data.

### Plugin

A collection of [records](#record) in a binary file with the extension `.esp`, `.esm`, or `.esl`. Also known as *files*, *data files*, or *modules*.

See also: [Data File - Creation Kit Wiki](https://www.creationkit.com/fallout4/index.php?title=Data_File)

## R

### Record

A record is a data structure in a [plugin](#plugin) identified by its [signature](#signature) and [Form ID](#form-id) that describes an object

### Record Header

The initial data structure of every [record](#record) that contains metadata about the record. The record header includes the record's [signature](#signature), data size, flags (such as deleted, [persistent](#persistent), compressed), [Form ID](#form-id), [form version](#form-version), and version control fields (VCS1, VCS2). Record headers are parsed before the record's actual data and provide essential information for xEdit to correctly interpret the record structure.

### Reference

A placed instance of an object in the game world, typically using the `REFR` signature (or `ACHR` for characters, `ACRE` for creatures). References link to a [base record](#base-record) that defines the object's properties, while the reference itself stores placement data (position, rotation, scale) and instance-specific flags like [Persistent](#persistent), [Initially Disabled](#initially-disabled), or [Visible When Distant](#visible-when-distant). For example, multiple sword references can all point to the same weapon base record.

### Resource

Game assets such as textures, 3D models, sounds, and other binary data files typically stored in BSA archives or loose files. Resources are referenced by records but stored separately from plugin data.

## S

### SHA1

Secure Hash Algorithm 1 - a cryptographic hash function that produces a 160-bit hash value. Like MD5, it's no longer recommended for security purposes but remains useful for file integrity checking and version control.

### Signature

An uppercase 4-character identifier that uniquely identifies a [record](#record) (e.g., `GLOB`, `NPC_`, `WEAP`) or [subrecord](#subrecord) (e.g., `EDID`, `LNAM`, `XCLL`) within a record. The signature is commonly, but not always, an abbreviation for the type of record or subrecord. For example, `GLOB` is always associated with a Global Variable record whereas `EDID` is always associated with the Editor ID subrecord, but `ANAM`, `BNAM`, `CNAM`, and so on do not have fixed meanings.

### STRINGS

Localized Strings - a binary file format (`.STRINGS`) used by Skyrim and later games to store externalized text strings in multiple languages. Part of the [localization](#localization) system alongside [DLSTRINGS](#dlstrings) and [ILSTRINGS](#ilstrings) files. STRINGS files contain general game text with limited length constraints.

### Subrecord

An [element](#element) with a [signature](#signature) that exists as data in the plugin itself

## T

### TGA

Truevision Targa - a raster graphics file format (`.tga`) used for texture storage in games. While [DDS](#dds) is more common in modern games for GPU-optimized textures, TGA files are still used for source artwork and in older games like Morrowind and Oblivion.

## V

### VCS

Version Control System - two fields (VCS1 and VCS2) stored in the [record header](#record-header) of [main records](#main-record) in some games. These fields were intended for internal Bethesda version tracking but are rarely used in practice. VCS values can be read and modified through scripting but generally don't affect game behavior.

### Visible When Distant

A flag on [reference](#reference) records that marks the placed object for [LOD](#lod) (Level of Detail) rendering. Objects with this flag generate distant LOD meshes so they remain visible at long distances, important for large structures and landmarks that should be visible from far away.

## W

### Winning Override

The final [overriding record](#overriding-record) in a chain of overrides across multiple plugins, determined by load order. The winning override is the version of the record that the game actually uses. For example, if a weapon record is modified by three different plugins, the version in the last-loading plugin becomes the winning override.

### Worldspace

A top-level container for exterior game world data. Worldspaces contain a grid of [exterior cells](#exterior-cell) that make up large outdoor environments. Each game has a main worldspace (e.g., "Tamriel" in Skyrim, "Commonwealth" in Fallout 4) and may include additional worldspaces for DLC areas or separate dimensions. Interior cells exist independently of worldspaces.

## X

### XWM

Xbox Wave Media - Bethesda's proprietary compressed audio format used in Skyrim and later games. XWM files use xWMA (Xbox Windows Media Audio) compression for efficient storage and streaming of sound effects, music, and dialogue. Often packaged inside [FUZ](#fuz) files for voice acting with lip-sync data.

