| Variable Name           | R/W       | Signature                        | Description                                                           |
|-------------------------|-----------|----------------------------------|-----------------------------------------------------------------------|
| `FileCount`             | Read Only | `FileCount: Integer`             | Returns the length of the array of loaded files in the active session |
| `FilterApplied`         | Read Only | `FilterApplied: Boolean`         | Returns whether a filter is applied                                   |
| `frmMain`               | Read Only | `frmMain: TForm`                 | Returns the main window object                                        |
| `wbAppName`             | Read Only | `wbAppName: String`              | Returns the game acronym for the active game mode                     |
| `wbDataPath`            | Read Only | `wbDataPath: String`             | Returns the full path to the game's Data folder                       |
| `wbDecodeTextureHashes` | Read Only | `wbDecodeTextureHashes: Boolean` | Returns whether Decode Texture Hashes is enabled                      |
| `wbGameMode`            | Read Only | `wbGameMode: TwbGameMode`        | Returns the active game mode                                          |
| `wbGameName`            | Read Only | `wbGameName: String`             | Returns the short game name for the active game mode                  |
| `wbGameName2`           | Read Only | `wbGameName2: String`            | Returns the long game name for the active game mode                   |
| `wbGameMasterEsm`       | Read Only | `wbGameMasterEsm: String`        | Returns the master file name for the active game mode                 |
| `wbLoadBSAs`            | Read Only | `wbLoadBSAs: Boolean`            | Returns whether Load BSAs is enabled                                  |
| `wbOutputPath`          | Read Only | `wbOutputPath: String`           | Returns the full path to the xEdit output folder                      |
| `wbProgramPath`         | Read Only | `wbProgramPath: String`          | Returns the full path to the xEdit executable                         |
| `wbRecordDefMap`        | Read Only | `wbRecordDefMap: TStringList`    | Returns a dictionary of record signatures and associated record defs  |
| `wbScriptsPath`         | Read Only | `wbScriptsPath: String`          | Returns the full path to the Edit Scripts folder                      |
| `wbSettings`            | Read Only | `wbSettings: TMemIniFile`        | Returns the xEdit settings file as a buffered TMemIniFile object      |
| `wbSettingsFileName`    | Read Only | `wbSettingsFileName: String`     | Returns the full path to the xEdit settings file                      |
| `wbSimpleRecords`       | Read Only | `wbSimpleRecords: Boolean`       | Returns whether Simple Records is enabled                             |
| `wbTempPath`            | Read Only | `wbTempPath: String`             | Returns the full path to the xEdit temp folder                        |
| `wbTrackAllEditorID`    | Read Only | `wbTrackAllEditorID: Boolean`    | Returns whether Track All Editor IDs is enabled                       |
| `wbVersionNumber`       | Read Only | `wbVersionNumber: Cardinal`      | Returns the xEdit version number                                      |

