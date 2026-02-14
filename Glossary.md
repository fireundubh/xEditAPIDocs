# Glossary

## B

### BSA

Bethesda Archive - a proprietary compressed archive format used by Bethesda Game Studios to package game assets (textures, models, sounds, etc.) for their games.

## C

### Container

Any [element](#element) that contains or can contain other elements

### CRC32

Cyclic Redundancy Check 32-bit - a hash function that produces a 32-bit checksum value used to detect accidental changes to raw data. Commonly used for verifying file integrity and resource archives.

## D

### DDS

DirectDraw Surface - a Microsoft image file format used for storing textures and environment maps. Widely used in video games for efficient GPU texture storage and supports various compression formats.

## E

### Editor ID

A human-readable string identifier not used by any game and intended for organizational purposes. However, [records](#record) whose [signature](#signature) is `GMST` are *uniquely* identified by Editor ID and will be overridden by later loading `GMST` records with matching Editor IDs.

### Element

All objects in xEdit are elements. There are two element archetypes:

- An element with a [signature](#signature) exists as data in the plugin itself. Also called a [subrecord](#subrecord).
- An element without a signature exists only in xEdit to represent the logical structure of parsed plugin data. These elements are not found in or saved to plugins.

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

## G

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

### Injected Record

A record whose [Load Order Form ID](#load-order-form-id) is unreserved but treated as contained by the file matching the specified [Mod ID](#mod-id) or [Light Mod ID](#light-mod-id).

When injected records with different [signatures](#signature) conflict, the game will crash.

## L

### Localization

The system for storing and retrieving translated game strings in language-specific files (.STRINGS, .DLSTRINGS, .ILSTRINGS). Allows games to support multiple languages by externalizing text content from plugin files.

### LOD

Level of Detail - simplified versions of 3D models and textures used at greater distances to improve rendering performance. LOD generation creates these optimized assets automatically from full-detail game data.

### Light Mod ID

A 3-character hexadecimal identifier for an ESL file associated with the [Object ID](#object-id) in a [Form ID](#form-id). The term "light" comes from nomenclature used to distinguish between slots into which plugins are loaded. ESL plugins are loaded into "light slots" and other plugins into "full slots."

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

### MD5

Message-Digest Algorithm 5 - a widely-used cryptographic hash function that produces a 128-bit hash value. While no longer considered secure for cryptographic purposes, it remains useful for file integrity verification and resource comparison.

### Master File

A [plugin](#plugin) on which another plugin depends. For a [record](#record) in a plugin to link to records outside its scope, that plugin must declare the source master files in its File Header. A plugin's master files has implications for its records' [File Form IDs](#file-form-id) and its load order.

### Master Record

A [record](#record) at the start of an [overriding record](#overriding-record) chain

### Mod ID

A 2-character hexadecimal identifier for an ESM or ESP plugin associated with the [Object ID](#object-id) in a [Form ID](#form-id)

## N

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

### Plugin

A collection of [records](#record) in a binary file with the extension `.esp`, `.esm`, or `.esl`. Also known as *files*, *data files*, or *modules*.

See also: [Data File - Creation Kit Wiki](https://www.creationkit.com/fallout4/index.php?title=Data_File)

## R

### Resource

Game assets such as textures, 3D models, sounds, and other binary data files typically stored in BSA archives or loose files. Resources are referenced by records but stored separately from plugin data.

### Record

A record is a data structure in a [plugin](#plugin) identified by its [signature](#signature) and [Form ID](#form-id) that describes an object

## S

### SHA1

Secure Hash Algorithm 1 - a cryptographic hash function that produces a 160-bit hash value. Like MD5, it's no longer recommended for security purposes but remains useful for file integrity checking and version control.

### Signature

An uppercase 4-character identifier that uniquely identifies a [record](#record) (e.g., `GLOB`, `NPC_`, `WEAP`) or [subrecord](#subrecord) (e.g., `EDID`, `LNAM`, `XCLL`) within a record. The signature is commonly, but not always, an abbreviation for the type of record or subrecord. For example, `GLOB` is always associated with a Global Variable record whereas `EDID` is always associated with the Editor ID subrecord, but `ANAM`, `BNAM`, `CNAM`, and so on do not have fixed meanings.

### Subrecord

An [element](#element) with a [signature](#signature) that exists as data in the plugin itself

