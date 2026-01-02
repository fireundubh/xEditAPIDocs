# Glossary

## C

### Container

Any [element](#element) that contains or can contain other elements

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

## H

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

### Master File

A [plugin](#plugin) on which another plugin depends. For a [record](#record) in a plugin to link to records outside its scope, that plugin must declare the source master files in its File Header. A plugin's master files has implications for its records' [File Form IDs](#file-form-id) and its load order.

### Master Record

A [record](#record) at the start of an [overriding record](#overriding-record) chain

### Mod ID

A 2-character hexadecimal identifier for an ESM or ESP plugin associated with the [Object ID](#object-id) in a [Form ID](#form-id)

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

### Record

A record is a data structure in a [plugin](#plugin) identified by its [signature](#signature) and [Form ID](#form-id) that describes an object

## S

### Signature

An uppercase 4-character identifier that uniquely identifies a [record](#record) (e.g., `GLOB`, `NPC_`, `WEAP`) or [subrecord](#subrecord) (e.g., `EDID`, `LNAM`, `XCLL`) within a record. The signature is commonly, but not always, an abbreviation for the type of record or subrecord. For example, `GLOB` is always associated with a Global Variable record whereas `EDID` is always associated with the Editor ID subrecord, but `ANAM`, `BNAM`, `CNAM`, and so on do not have fixed meanings.

### Subrecord

An [element](#element) with a [signature](#signature) that exists as data in the plugin itself
