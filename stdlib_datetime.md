# Date & Time Reference

Functions for working with dates, times, formatting, and calendar calculations.

**Unit:** SysUtils

[← Back to Standard Library Overview](stdlib_home.md)

## Table of Contents

- [Current Date and Time](#current-date-and-time)
- [Creating Dates and Times](#creating-dates-and-times)
- [Extracting Date/Time Parts](#extracting-datetime-parts)
- [Formatting](#formatting)
- [Parsing](#parsing)
- [Date Calculations](#date-calculations)
- [Time Calculations](#time-calculations)
- [Conversion](#conversion)

## Understanding TDateTime

**TDateTime** is a floating-point type where:
- **Integer part** = number of days since 1899-12-30
- **Fractional part** = fraction of a 24-hour day

```pascal
// Examples:
0.0     // 1899-12-30 00:00:00
1.0     // 1899-12-31 00:00:00
0.5     // 1899-12-30 12:00:00 (noon)
2.75    // 1900-01-01 18:00:00 (6 PM)
```

## Current Date and Time

| Function | Signature | Description |
|----------|-----------|-------------|
| `Now` | `Now(): TDateTime` | Current date and time |
| `Date` | `Date(): TDateTime` | Current date (time = 00:00:00) |
| `Time` | `Time(): TDateTime` | Current time (date = day 0) |

### Examples

```pascal
var
  dt: TDateTime;
begin
  dt := Now();
  AddMessage('Current date/time: ' + DateTimeToStr(dt));

  dt := Date();
  AddMessage('Current date: ' + DateToStr(dt));

  dt := Time();
  AddMessage('Current time: ' + TimeToStr(dt));
end;
```

### xEdit Example: Timestamp Script Execution
```pascal
// Log script start and end times
var
  startTime, endTime: TDateTime;
  elapsed: Extended;
begin
  startTime := Now();
  AddMessage('Script started: ' + FormatDateTime('yyyy-mm-dd hh:nn:ss', startTime));

  // ... do work ...

  endTime := Now();
  elapsed := (endTime - startTime) * 24 * 60;  // Convert to minutes

  AddMessage('Script completed: ' + FormatDateTime('yyyy-mm-dd hh:nn:ss', endTime));
  AddMessage(Format('Elapsed time: %.2f minutes', [elapsed]));
end;
```

## Creating Dates and Times

| Function | Signature | Description |
|----------|-----------|-------------|
| `EncodeDate` | `EncodeDate(Year, Month, Day: Word): TDateTime` | Create date from components |
| `EncodeTime` | `EncodeTime(Hour, Min, Sec, MSec: Word): TDateTime` | Create time from components |
| `EncodeDateTime` | `EncodeDateTime(Y, M, D, H, Min, S, MS: Word): TDateTime` | Create date and time |

### Examples

```pascal
var
  dt: TDateTime;
begin
  // Create specific date
  dt := EncodeDate(2024, 12, 25);  // Christmas 2024
  AddMessage('Date: ' + DateToStr(dt));

  // Create specific time
  dt := EncodeTime(14, 30, 0, 0);  // 2:30 PM
  AddMessage('Time: ' + TimeToStr(dt));

  // Create specific date and time
  dt := EncodeDateTime(2024, 12, 25, 14, 30, 0, 0);  // Christmas 2024 at 2:30 PM
  AddMessage('DateTime: ' + DateTimeToStr(dt));
end;
```

### xEdit Example: Schedule Tasks
```pascal
// Check if current time is within maintenance window
var
  currentTime, startTime, endTime: TDateTime;
  inWindow: Boolean;
begin
  currentTime := Time();
  startTime := EncodeTime(2, 0, 0, 0);   // 2:00 AM
  endTime := EncodeTime(4, 0, 0, 0);     // 4:00 AM

  inWindow := (currentTime >= startTime) and (currentTime <= endTime);

  if inWindow then
    AddMessage('Currently in maintenance window')
  else
    AddMessage('Outside maintenance window');
end;
```

## Extracting Date/Time Parts

| Function | Signature | Description |
|----------|-----------|-------------|
| `DecodeDate` | `DecodeDate(Date: TDateTime, var Y, M, D: Word)` | Extract year, month, day |
| `DecodeTime` | `DecodeTime(Time: TDateTime, var H, Min, S, MS: Word)` | Extract hour, minute, second, millisecond |
| `DecodeDateTime` | `DecodeDateTime(DT: TDateTime, var Y, M, D, H, Min, S, MS: Word)` | Extract all components |
| `DayOfWeek` | `DayOfWeek(Date: TDateTime): Integer` | Day of week (1=Sunday, 7=Saturday) |
| `DayOfTheWeek` | `DayOfTheWeek(Date: TDateTime): Integer` | Day of week (1=Monday, 7=Sunday) |
| `DayOfYear` | `DayOfYear(Date: TDateTime): Integer` | Day number in year (1-366) |
| `WeekOf` | `WeekOf(Date: TDateTime): Integer` | Week number in year |
| `MonthOf` | `MonthOf(Date: TDateTime): Integer` | Month (1-12) |
| `YearOf` | `YearOf(Date: TDateTime): Integer` | Year |

### Examples

```pascal
var
  dt: TDateTime;
  year, month, day: Word;
  hour, min, sec, msec: Word;
  dow: Integer;
begin
  dt := Now();

  // Extract date components
  DecodeDate(dt, year, month, day);
  AddMessage(Format('Date: %d-%02d-%02d', [year, month, day]));

  // Extract time components
  DecodeTime(dt, hour, min, sec, msec);
  AddMessage(Format('Time: %02d:%02d:%02d.%03d', [hour, min, sec, msec]));

  // Get day of week
  dow := DayOfWeek(dt);
  case dow of
    1: AddMessage('Today is Sunday');
    2: AddMessage('Today is Monday');
    // ... etc
    7: AddMessage('Today is Saturday');
  end;
end;
```

### xEdit Example: Organize Output by Date
```pascal
// Create output directory based on current date
var
  dt: TDateTime;
  year, month, day: Word;
  outputDir: string;
begin
  dt := Date();
  DecodeDate(dt, year, month, day);

  outputDir := Format('%sOutput\%d\%02d\%02d\', [
    wbDataPath,
    year,
    month,
    day
  ]);

  if not DirectoryExists(outputDir) then
    ForceDirectories(outputDir);

  AddMessage('Output directory: ' + outputDir);
end;
```

## Formatting

### FormatDateTime

**Signature:** `FormatDateTime(Format: string, DateTime: TDateTime): string`

Format dates and times using format specifiers.

#### Date Format Specifiers

| Specifier | Description | Example (2024-12-25) |
|-----------|-------------|---------------------|
| `d` | Day without leading zero | `25` |
| `dd` | Day with leading zero | `25` |
| `ddd` | Day name abbreviated | `Wed` |
| `dddd` | Day name full | `Wednesday` |
| `m` | Month without leading zero | `12` |
| `mm` | Month with leading zero | `12` |
| `mmm` | Month name abbreviated | `Dec` |
| `mmmm` | Month name full | `December` |
| `yy` | Year 2-digit | `24` |
| `yyyy` | Year 4-digit | `2024` |

#### Time Format Specifiers

| Specifier | Description | Example (14:05:07.123) |
|-----------|-------------|------------------------|
| `h` | Hour 12-hour without zero | `2` |
| `hh` | Hour 12-hour with zero | `02` |
| `n` | Minute without zero | `5` |
| `nn` | Minute with zero | `05` |
| `s` | Second without zero | `7` |
| `ss` | Second with zero | `07` |
| `z` | Millisecond without zero | `123` |
| `zzz` | Millisecond with zero | `123` |
| `am/pm` | Display AM/PM | `PM` |
| `a/p` | Display A/P | `P` |

#### Common Format Patterns

```pascal
FormatDateTime('yyyy-mm-dd', Now())                    // 2024-12-25
FormatDateTime('dd/mm/yyyy', Now())                    // 25/12/2024
FormatDateTime('mmmm d, yyyy', Now())                  // December 25, 2024
FormatDateTime('hh:nn:ss', Now())                      // 14:05:07
FormatDateTime('hh:nn:ss am/pm', Now())                // 02:05:07 PM
FormatDateTime('yyyy-mm-dd hh:nn:ss', Now())           // 2024-12-25 14:05:07
FormatDateTime('dddd, mmmm d, yyyy "at" h:nn am/pm', Now()) // Wednesday, December 25, 2024 at 2:05 PM
```

### Other Formatting Functions

| Function | Signature | Description |
|----------|-----------|-------------|
| `DateToStr` | `DateToStr(Date: TDateTime): string` | Format date using system format |
| `TimeToStr` | `TimeToStr(Time: TDateTime): string` | Format time using system format |
| `DateTimeToStr` | `DateTimeToStr(DateTime: TDateTime): string` | Format date/time using system format |

### xEdit Formatting Examples

#### Create Timestamped Log File
```pascal
// Generate log filename with timestamp
var
  logPath, timestamp: string;
  log: TStringList;
begin
  timestamp := FormatDateTime('yyyymmdd_hhnnss', Now());
  logPath := Format('%sLogs\log_%s.txt', [wbDataPath, timestamp]);

  log := TStringList.Create;
  try
    log.Add(Format('Log created: %s', [FormatDateTime('yyyy-mm-dd hh:nn:ss', Now())]));
    log.Add('---');
    // Add log entries...

    ForceDirectories(ExtractFilePath(logPath));
    log.SaveToFile(logPath);
    AddMessage('Log saved: ' + logPath);
  finally
    log.Free;
  end;
end;
```

#### Display Human-Readable Timestamps
```pascal
// Format various timestamps for display
var
  dt: TDateTime;
begin
  dt := Now();

  AddMessage('ISO 8601: ' + FormatDateTime('yyyy-mm-dd"T"hh:nn:ss', dt));
  AddMessage('US Format: ' + FormatDateTime('mm/dd/yyyy hh:nn am/pm', dt));
  AddMessage('European: ' + FormatDateTime('dd.mm.yyyy hh:nn', dt));
  AddMessage('Full: ' + FormatDateTime('dddd, mmmm d, yyyy "at" h:nn:ss am/pm', dt));
  AddMessage('Time only: ' + FormatDateTime('hh:nn:ss', dt));
  AddMessage('Date only: ' + FormatDateTime('yyyy-mm-dd', dt));
end;
```

## Parsing

Convert strings back to TDateTime values.

| Function | Signature | Description |
|----------|-----------|-------------|
| `StrToDate` | `StrToDate(S: string): TDateTime` | Parse date string (raises exception on error) |
| `StrToTime` | `StrToTime(S: string): TDateTime` | Parse time string (raises exception on error) |
| `StrToDateTime` | `StrToDateTime(S: string): TDateTime` | Parse date/time string (raises exception on error) |
| `TryStrToDate` | `TryStrToDate(S: string, var Value: TDateTime): Boolean` | Safe date parsing |
| `TryStrToTime` | `TryStrToTime(S: string, var Value: TDateTime): Boolean` | Safe time parsing |
| `TryStrToDateTime` | `TryStrToDateTime(S: string, var Value: TDateTime): Boolean` | Safe date/time parsing |

### Example: Parse User Input
```pascal
// Parse date from user input
var
  input: string;
  dt: TDateTime;
begin
  if InputQuery('Enter Date', 'Date (YYYY-MM-DD):', input) then begin
    if TryStrToDate(input, dt) then
      AddMessage('Parsed: ' + DateToStr(dt))
    else
      MessageDlg('Invalid date format', mtError, [mbOK], 0);
  end;
end;
```

## Date Calculations

| Function | Signature | Description |
|----------|-----------|-------------|
| `IncMonth` | `IncMonth(Date: TDateTime, NumberOfMonths: Integer): TDateTime` | Add/subtract months |
| `IncYear` | `IncYear(Date: TDateTime, NumberOfYears: Integer): TDateTime` | Add/subtract years |
| `IncDay` | `IncDay(Date: TDateTime, NumberOfDays: Integer): TDateTime` | Add/subtract days |
| `IncWeek` | `IncWeek(Date: TDateTime, NumberOfWeeks: Integer): TDateTime` | Add/subtract weeks |
| `DaysBetween` | `DaysBetween(Date1, Date2: TDateTime): Integer` | Days between dates |
| `MonthsBetween` | `MonthsBetween(Date1, Date2: TDateTime): Integer` | Months between dates |
| `YearsBetween` | `YearsBetween(Date1, Date2: TDateTime): Integer` | Years between dates |
| `IsLeapYear` | `IsLeapYear(Year: Word): Boolean` | Check if leap year |
| `DaysInMonth` | `DaysInMonth(Date: TDateTime): Integer` | Number of days in month |
| `DaysInYear` | `DaysInYear(Year: Word): Integer` | Number of days in year (365 or 366) |

### Examples

```pascal
var
  today, future, past: TDateTime;
  days: Integer;
begin
  today := Date();

  // Add time periods
  future := IncMonth(today, 6);    // 6 months from now
  AddMessage('In 6 months: ' + DateToStr(future));

  future := IncYear(today, 1);     // 1 year from now
  AddMessage('In 1 year: ' + DateToStr(future));

  future := IncDay(today, 30);     // 30 days from now
  AddMessage('In 30 days: ' + DateToStr(future));

  // Calculate difference
  past := EncodeDate(2020, 1, 1);
  days := DaysBetween(today, past);
  AddMessage(Format('Days since 2020-01-01: %d', [days]));

  // Check leap year
  if IsLeapYear(2024) then
    AddMessage('2024 is a leap year');
end;
```

### xEdit Example: Schedule Maintenance
```pascal
// Calculate next maintenance date (first Monday of next month)
function NextMaintenanceDate(fromDate: TDateTime): TDateTime;
var
  nextMonth: TDateTime;
  firstDay, dow: Integer;
begin
  // Go to first day of next month
  nextMonth := IncMonth(fromDate, 1);
  DecodeDate(nextMonth, year, month, day);
  nextMonth := EncodeDate(year, month, 1);

  // Find first Monday (DayOfWeek: 1=Sun, 2=Mon, ...)
  dow := DayOfWeek(nextMonth);
  if dow = 2 then
    Result := nextMonth  // Already Monday
  else if dow = 1 then
    Result := IncDay(nextMonth, 1)  // Sunday, add 1 day
  else
    Result := IncDay(nextMonth, 9 - dow);  // Calculate days to Monday
end;
```

## Time Calculations

| Function | Signature | Description |
|----------|-----------|-------------|
| `IncHour` | `IncHour(Time: TDateTime, NumberOfHours: Integer): TDateTime` | Add/subtract hours |
| `IncMinute` | `IncMinute(Time: TDateTime, NumberOfMinutes: Integer): TDateTime` | Add/subtract minutes |
| `IncSecond` | `IncSecond(Time: TDateTime, NumberOfSeconds: Integer): TDateTime` | Add/subtract seconds |
| `IncMilliSecond` | `IncMilliSecond(Time: TDateTime, NumberOfMilliSeconds: Int64): TDateTime` | Add/subtract milliseconds |
| `HoursBetween` | `HoursBetween(Time1, Time2: TDateTime): Int64` | Hours between times |
| `MinutesBetween` | `MinutesBetween(Time1, Time2: TDateTime): Int64` | Minutes between times |
| `SecondsBetween` | `SecondsBetween(Time1, Time2: TDateTime): Int64` | Seconds between times |
| `MilliSecondsBetween` | `MilliSecondsBetween(Time1, Time2: TDateTime): Int64` | Milliseconds between times |

### Examples

```pascal
var
  startTime, endTime: TDateTime;
  elapsed: Int64;
begin
  startTime := Now();

  // ... do work ...

  endTime := Now();

  // Calculate elapsed time
  elapsed := SecondsBetween(endTime, startTime);
  AddMessage(Format('Elapsed: %d seconds', [elapsed]));

  elapsed := MilliSecondsBetween(endTime, startTime);
  AddMessage(Format('Elapsed: %d milliseconds', [elapsed]));
end;
```

### xEdit Example: Performance Timing
```pascal
// Measure performance of different operations
var
  startTime, endTime: TDateTime;
  elapsedMs: Int64;
  i: Integer;
begin
  AddMessage('Performance test starting...');

  // Test operation 1
  startTime := Now();
  for i := 0 to 999999 do begin
    // Do something...
  end;
  endTime := Now();
  elapsedMs := MilliSecondsBetween(endTime, startTime);
  AddMessage(Format('Operation 1: %d ms', [elapsedMs]));

  // Test operation 2
  startTime := Now();
  for i := 0 to 999999 do begin
    // Do something else...
  end;
  endTime := Now();
  elapsedMs := MilliSecondsBetween(endTime, startTime);
  AddMessage(Format('Operation 2: %d ms', [elapsedMs]));
end;
```

## Conversion

| Function | Signature | Description |
|----------|-----------|-------------|
| `DateTimeToTimeStamp` | `DateTimeToTimeStamp(DateTime: TDateTime): TTimeStamp` | Convert to timestamp record |
| `TimeStampToDateTime` | `TimeStampToDateTime(TimeStamp: TTimeStamp): TDateTime` | Convert from timestamp record |
| `DateTimeToFileDate` | `DateTimeToFileDate(DateTime: TDateTime): Integer` | Convert to DOS file date |
| `FileDateToDateTime` | `FileDateToDateTime(FileDate: Integer): TDateTime` | Convert from DOS file date |
| `DateTimeToStr` | `DateTimeToStr(DateTime: TDateTime): string` | Convert to string |

### TTimeStamp Record

```pascal
TTimeStamp = record
  Time: Integer;  // Milliseconds since midnight
  Date: Integer;  // Days since 1/1/0001
end;
```

---

[← Back to Standard Library Overview](stdlib_home.md) | [Next: Mathematics →](stdlib_math.md)
