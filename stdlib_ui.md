# UI Components Reference

User interface components for creating dialogs, forms, and interactive controls in xEdit scripts.

**Units:** Dialogs, Forms, Controls, StdCtrls, ComCtrls, ExtCtrls, Buttons, Menus

[← Back to Standard Library Overview](stdlib_home.md)

## Table of Contents

- [Dialog Functions](#dialog-functions)
- [Application and Screen](#application-and-screen)
- [Form Creation and Management](#form-creation-and-management)
- [Standard Controls](#standard-controls)
- [Common Controls](#common-controls)
- [Extended Controls](#extended-controls)
- [Menus](#menus)
- [File Dialogs](#file-dialogs)
- [Complete Form Examples](#complete-form-examples)

## Dialog Functions

Simple dialog functions for quick user interaction.

| Function | Signature | Description |
|----------|-----------|-------------|
| `ShowMessage` | `ShowMessage(Msg: string)` | Display simple message box |
| `MessageDlg` | `MessageDlg(Msg: string, DlgType: TMsgDlgType, Buttons: TMsgDlgButtons, HelpCtx: Longint): Integer` | Display message with custom buttons |
| `MessageDlgPos` | `MessageDlgPos(Msg: string, DlgType: TMsgDlgType, Buttons: TMsgDlgButtons, HelpCtx: Longint, X, Y: Integer): Integer` | Message dialog at position |
| `InputQuery` | `InputQuery(Caption, Prompt: string, var Value: string): Boolean` | Get string input from user |
| `InputBox` | `InputBox(Caption, Prompt, Default: string): string` | Get string input (simpler) |

### Dialog Type Constants

```pascal
TMsgDlgType = (mtWarning, mtError, mtInformation, mtConfirmation, mtCustom);
```

### Dialog Button Constants

```pascal
mbYes, mbNo, mbOK, mbCancel, mbAbort, mbRetry, mbIgnore, mbAll, mbHelp
```

**Button sets:**
```pascal
[mbYes, mbNo]        // Yes/No buttons
[mbOK, mbCancel]     // OK/Cancel buttons
[mbOK]               // OK button only
```

### Dialog Result Constants

```pascal
mrNone = 0;
mrOk = idOk;
mrCancel = idCancel;
mrAbort = idAbort;
mrRetry = idRetry;
mrIgnore = idIgnore;
mrYes = idYes;
mrNo = idNo;
mrAll = mrYes + 1;
```

### xEdit Dialog Examples

#### Confirm Action
```pascal
// Ask user for confirmation
var
  response: Integer;
begin
  response := MessageDlg(
    'Delete all records of type NPC_?',
    mtConfirmation,
    [mbYes, mbNo],
    0
  );

  if response = mrYes then
    AddMessage('User confirmed deletion')
  else
    AddMessage('User cancelled');
end;
```

#### Get User Input
```pascal
// Get EditorID prefix from user
var
  prefix: string;
begin
  if InputQuery('Enter Prefix', 'EditorID prefix:', prefix) then begin
    prefix := Trim(prefix);
    if prefix <> '' then
      AddMessage('Using prefix: ' + prefix)
    else
      ShowMessage('Prefix cannot be empty');
  end;
end;
```

#### Error Notification
```pascal
// Show error message
procedure ShowError(const msg: string);
begin
  MessageDlg('ERROR: ' + msg, mtError, [mbOK], 0);
end;

// Usage
if not FileExists(pluginPath) then
  ShowError('Plugin file not found: ' + pluginPath);
```

## Application and Screen

Global application and screen objects.

### TApplication

Global variable: `Application`

| Property/Method | Type | Description |
|----------------|------|-------------|
| `Title` | string | Application title |
| `ProcessMessages` | procedure | Process pending messages (keep UI responsive) |
| `Terminate` | procedure | Close application |
| `MessageBox` | function | Show Windows message box |

### TScreen

Global variable: `Screen`

| Property | Type | Description |
|----------|------|-------------|
| `Width` | Integer | Screen width in pixels |
| `Height` | Integer | Screen height in pixels |
| `Cursor` | TCursor | Current cursor |
| `Cursors[Index]` | HCURSOR | Cursor handles |

### Cursor Constants

```pascal
crDefault = 0;
crNone = -1;
crArrow = -2;
crCross = -3;
crIBeam = -4;
crSize = -22;
crSizeNESW = -6;
crSizeNS = -7;
crSizeNWSE = -8;
crSizeWE = -9;
crUpArrow = -10;
crHourGlass = -11;
crDrag = -12;
crNoDrop = -13;
crHSplit = -14;
crVSplit = -15;
crHandPoint = -21;
crHelp = -20;
```

### Example: Keep UI Responsive
```pascal
// Process long-running operation
var
  i: Integer;
begin
  for i := 0 to 10000 do begin
    // Process record...

    if (i mod 100) = 0 then
      Application.ProcessMessages;  // Keep UI responsive
  end;
end;
```

## Form Creation and Management

### TForm

Forms are the main windows of your application.

**Constructor:**
```pascal
form := TForm.Create(nil);  // nil = no owner
```

#### Key Properties

| Property | Type | Description |
|----------|------|-------------|
| `Caption` | string | Window title |
| `Width` | Integer | Form width in pixels |
| `Height` | Integer | Form height in pixels |
| `Left` | Integer | X position on screen |
| `Top` | Integer | Y position on screen |
| `ClientWidth` | Integer | Client area width |
| `ClientHeight` | Integer | Client area height |
| `Position` | TPosition | Form position (poScreenCenter, poDesktopCenter, poMainFormCenter, poDesigned) |
| `BorderStyle` | TFormBorderStyle | Border style (bsDialog, bsSingle, bsSizeable, bsNone) |
| `FormStyle` | TFormStyle | Form style (fsNormal, fsMDIChild, fsMDIForm, fsStayOnTop) |
| `WindowState` | TWindowState | Window state (wsNormal, wsMinimized, wsMaximized) |
| `Visible` | Boolean | Visibility |
| `Enabled` | Boolean | Enabled state |
| `Color` | TColor | Background color |
| `Font` | TFont | Default font |

#### Key Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `Show` | `Show()` | Show form non-modally |
| `ShowModal` | `ShowModal(): Integer` | Show form modally (waits for close) |
| `Close` | `Close()` | Close form |
| `Hide` | `Hide()` | Hide form |
| `SetFocus` | `SetFocus()` | Give form focus |
| `Refresh` | `Refresh()` | Repaint form |

### Form Position Constants

```pascal
poDesigned        // Use designed position
poDefault         // Default position
poDefaultPosOnly  // Default position, designed size
poDefaultSizeOnly // Designed position, default size
poScreenCenter    // Center on screen
poDesktopCenter   // Center on desktop
poMainFormCenter  // Center on main form
poOwnerFormCenter // Center on owner form
```

### Form Border Style Constants

```pascal
bsNone       // No border
bsSingle     // Single border, not resizable
bsSizeable   // Sizable border
bsDialog     // Dialog border
bsToolWindow // Tool window
bsSizeToolWin // Sizable tool window
```

## Standard Controls

Controls from the StdCtrls unit.

### TLabel

Display static text.

```pascal
lbl := TLabel.Create(form);
lbl.Parent := form;
lbl.Caption := 'Enter name:';
lbl.Left := 10;
lbl.Top := 10;
```

| Property | Type | Description |
|----------|------|-------------|
| `Caption` | string | Text to display |
| `Alignment` | TAlignment | Text alignment (taLeftJustify, taRightJustify, taCenter) |
| `WordWrap` | Boolean | Word wrap |
| `AutoSize` | Boolean | Auto-size to fit text |
| `Transparent` | Boolean | Transparent background |

### TEdit

Single-line text input.

```pascal
edit := TEdit.Create(form);
edit.Parent := form;
edit.Left := 10;
edit.Top := 30;
edit.Width := 200;
edit.Text := 'Default value';
```

| Property | Type | Description |
|----------|------|-------------|
| `Text` | string | Current text |
| `MaxLength` | Integer | Maximum length (0 = unlimited) |
| `ReadOnly` | Boolean | Read-only mode |
| `PasswordChar` | Char | Password character (e.g., '*') |
| `CharCase` | TEditCharCase | Character case (ecNormal, ecUpperCase, ecLowerCase) |

### TMemo

Multi-line text editor.

```pascal
memo := TMemo.Create(form);
memo.Parent := form;
memo.Left := 10;
memo.Top := 60;
memo.Width := 400;
memo.Height := 200;
memo.ScrollBars := ssVertical;
```

| Property | Type | Description |
|----------|------|-------------|
| `Lines` | TStrings | Text lines (TStringList) |
| `Text` | string | All text as single string |
| `ScrollBars` | TScrollStyle | Scroll bars (ssNone, ssHorizontal, ssVertical, ssBoth) |
| `WordWrap` | Boolean | Word wrap |
| `WantTabs` | Boolean | Accept tab key |
| `WantReturns` | Boolean | Accept return key |

**TStrings methods:** See [Data Structures Reference](stdlib_data.md#tstrings-and-tstringlist)

### TButton

Clickable button.

```pascal
btn := TButton.Create(form);
btn.Parent := form;
btn.Caption := 'Process Records';
btn.Left := 10;
btn.Top := 270;
btn.Width := 120;
btn.OnClick := @ButtonClick;  // Assign event handler
```

| Property | Type | Description |
|----------|------|-------------|
| `Caption` | string | Button text |
| `Default` | Boolean | Default button (Enter key) |
| `Cancel` | Boolean | Cancel button (Esc key) |
| `ModalResult` | TModalResult | Modal result when clicked |

### TCheckBox

Checkbox control.

```pascal
chk := TCheckBox.Create(form);
chk.Parent := form;
chk.Caption := 'Include deleted records';
chk.Left := 10;
chk.Top := 300;
chk.Checked := False;
```

| Property | Type | Description |
|----------|------|-------------|
| `Checked` | Boolean | Checked state |
| `State` | TCheckBoxState | Three-state (cbUnchecked, cbChecked, cbGrayed) |
| `AllowGrayed` | Boolean | Allow grayed state |

### TRadioButton

Radio button (mutually exclusive in group).

```pascal
rb1 := TRadioButton.Create(form);
rb1.Parent := form;
rb1.Caption := 'Option 1';
rb1.Checked := True;
rb1.Left := 10;
rb1.Top := 330;
```

| Property | Type | Description |
|----------|------|-------------|
| `Checked` | Boolean | Selected state |

### TListBox

List of items.

```pascal
listBox := TListBox.Create(form);
listBox.Parent := form;
listBox.Left := 10;
listBox.Top := 60;
listBox.Width := 200;
listBox.Height := 200;
listBox.Items.Add('Item 1');
listBox.Items.Add('Item 2');
```

| Property | Type | Description |
|----------|------|-------------|
| `Items` | TStrings | List items |
| `ItemIndex` | Integer | Selected item index (-1 = none) |
| `MultiSelect` | Boolean | Allow multiple selection |
| `Sorted` | Boolean | Auto-sort items |
| `Selected[Index]` | Boolean | Selection state (multi-select) |

### TComboBox

Dropdown list.

```pascal
combo := TComboBox.Create(form);
combo.Parent := form;
combo.Left := 10;
combo.Top := 90;
combo.Width := 200;
combo.Items.Add('Option 1');
combo.Items.Add('Option 2');
combo.ItemIndex := 0;
```

| Property | Type | Description |
|----------|------|-------------|
| `Items` | TStrings | Dropdown items |
| `ItemIndex` | Integer | Selected item index |
| `Text` | string | Current text |
| `Style` | TComboBoxStyle | Style (csDropDown, csSimple, csDropDownList, csOwnerDrawFixed, csOwnerDrawVariable) |

## Common Controls

Controls from the ComCtrls unit.

### TProgressBar

Progress indicator.

```pascal
progress := TProgressBar.Create(form);
progress.Parent := form;
progress.Left := 10;
progress.Top := 350;
progress.Width := 400;
progress.Min := 0;
progress.Max := 100;
progress.Position := 0;
```

| Property | Type | Description |
|----------|------|-------------|
| `Min` | Integer | Minimum value |
| `Max` | Integer | Maximum value |
| `Position` | Integer | Current position |
| `Step` | Integer | Step increment |

| Method | Signature | Description |
|--------|-----------|-------------|
| `StepIt` | `StepIt()` | Advance by Step amount |
| `StepBy` | `StepBy(Delta: Integer)` | Advance by amount |

### TStatusBar

Status bar at bottom of form.

```pascal
statusBar := TStatusBar.Create(form);
statusBar.Parent := form;
statusBar.SimpleText := 'Ready';
```

| Property | Type | Description |
|----------|------|-------------|
| `SimpleText` | string | Simple text mode |
| `SimplePanel` | Boolean | Use simple panel |
| `Panels` | TStatusPanels | Multiple panels |

### TPageControl and TTabSheet

Tabbed interface.

```pascal
pageControl := TPageControl.Create(form);
pageControl.Parent := form;
pageControl.Align := alClient;

// Add tab page
tabSheet1 := TTabSheet.Create(pageControl);
tabSheet1.PageControl := pageControl;
tabSheet1.Caption := 'General';

tabSheet2 := TTabSheet.Create(pageControl);
tabSheet2.PageControl := pageControl;
tabSheet2.Caption := 'Advanced';
```

**TPageControl properties:**

| Property | Type | Description |
|----------|------|-------------|
| `ActivePage` | TTabSheet | Active page |
| `PageCount` | Integer | Number of pages |
| `Pages[Index]` | TTabSheet | Page by index |
| `TabIndex` | Integer | Active tab index |

**TTabSheet properties:**

| Property | Type | Description |
|----------|------|-------------|
| `Caption` | string | Tab caption |
| `PageControl` | TPageControl | Parent page control |
| `PageIndex` | Integer | Tab position |

### TTreeView

Hierarchical tree view.

```pascal
tree := TTreeView.Create(form);
tree.Parent := form;
tree.Left := 10;
tree.Top := 60;
tree.Width := 250;
tree.Height := 300;

// Add nodes
node1 := tree.Items.Add(nil, 'Root');
node2 := tree.Items.AddChild(node1, 'Child 1');
node3 := tree.Items.AddChild(node1, 'Child 2');
```

| Property | Type | Description |
|----------|------|-------------|
| `Items` | TTreeNodes | Tree nodes |
| `Selected` | TTreeNode | Selected node |
| `ShowButtons` | Boolean | Show expand/collapse buttons |
| `ShowLines` | Boolean | Show connecting lines |
| `ShowRoot` | Boolean | Show root lines |

**TTreeNodes methods:**

| Method | Signature | Description |
|--------|-----------|-------------|
| `Add` | `Add(Node: TTreeNode, S: string): TTreeNode` | Add sibling node |
| `AddChild` | `AddChild(Node: TTreeNode, S: string): TTreeNode` | Add child node |
| `Clear` | `Clear()` | Remove all nodes |

**TTreeNode properties:**

| Property | Type | Description |
|----------|------|-------------|
| `Text` | string | Node text |
| `Parent` | TTreeNode | Parent node |
| `Count` | Integer | Child count |
| `Item[Index]` | TTreeNode | Child node |
| `Expanded` | Boolean | Expanded state |
| `Selected` | Boolean | Selected state |

### TListView

List view with columns.

```pascal
listView := TListView.Create(form);
listView.Parent := form;
listView.Left := 10;
listView.Top := 60;
listView.Width := 500;
listView.Height := 300;
listView.ViewStyle := vsReport;

// Add columns
col := listView.Columns.Add;
col.Caption := 'EditorID';
col.Width := 200;

col := listView.Columns.Add;
col.Caption := 'FormID';
col.Width := 100;

// Add item
item := listView.Items.Add;
item.Caption := 'MyRecord';
item.SubItems.Add('01000ABC');
```

| Property | Type | Description |
|----------|------|-------------|
| `Columns` | TListColumns | Column definitions |
| `Items` | TListItems | List items |
| `ViewStyle` | TViewStyle | View style (vsIcon, vsSmallIcon, vsList, vsReport) |
| `Selected` | TListItem | Selected item |

## Extended Controls

Controls from the ExtCtrls unit.

### TPanel

Container panel.

```pascal
panel := TPanel.Create(form);
panel.Parent := form;
panel.Left := 10;
panel.Top := 10;
panel.Width := 400;
panel.Height := 300;
panel.Caption := '';
panel.BevelOuter := bvLowered;
```

| Property | Type | Description |
|----------|------|-------------|
| `Align` | TAlign | Alignment (alNone, alTop, alBottom, alLeft, alRight, alClient) |
| `Caption` | string | Panel text |
| `BevelOuter` | TPanelBevel | Outer bevel (bvNone, bvLowered, bvRaised) |
| `BevelInner` | TPanelBevel | Inner bevel |

### TImage

Display images.

```pascal
img := TImage.Create(form);
img.Parent := form;
img.Left := 10;
img.Top := 10;
img.Width := 200;
img.Height := 200;
img.Stretch := True;
img.Picture.LoadFromFile('image.bmp');
```

| Property | Type | Description |
|----------|------|-------------|
| `Picture` | TPicture | Image content |
| `Stretch` | Boolean | Stretch to fit |
| `Proportional` | Boolean | Keep aspect ratio |
| `Center` | Boolean | Center image |
| `Transparent` | Boolean | Transparent |

### TTimer

Execute code at intervals.

```pascal
timer := TTimer.Create(form);
timer.Interval := 1000;  // milliseconds
timer.OnTimer := @TimerTick;
timer.Enabled := True;
```

| Property | Type | Description |
|----------|------|-------------|
| `Enabled` | Boolean | Timer enabled |
| `Interval` | Cardinal | Interval in milliseconds |

### TSplitter

Resizable splitter.

```pascal
splitter := TSplitter.Create(form);
splitter.Parent := form;
splitter.Align := alLeft;
splitter.Width := 4;
```

| Property | Type | Description |
|----------|------|-------------|
| `Align` | TAlign | Alignment |
| `MinSize` | Integer | Minimum size |

## Menus

### TMainMenu

Main menu bar.

```pascal
mainMenu := TMainMenu.Create(form);
form.Menu := mainMenu;

// Add menu items
fileMenu := TMenuItem.Create(mainMenu);
fileMenu.Caption := '&File';
mainMenu.Items.Add(fileMenu);

openItem := TMenuItem.Create(fileMenu);
openItem.Caption := '&Open...';
openItem.OnClick := @OpenClick;
fileMenu.Add(openItem);

// Separator
sepItem := TMenuItem.Create(fileMenu);
sepItem.Caption := '-';
fileMenu.Add(sepItem);

exitItem := TMenuItem.Create(fileMenu);
exitItem.Caption := 'E&xit';
exitItem.OnClick := @ExitClick;
fileMenu.Add(exitItem);
```

### TPopupMenu

Context menu.

```pascal
popupMenu := TPopupMenu.Create(form);
listView.PopupMenu := popupMenu;

menuItem := TMenuItem.Create(popupMenu);
menuItem.Caption := 'Delete';
menuItem.OnClick := @DeleteClick;
popupMenu.Items.Add(menuItem);
```

### TMenuItem

Menu item.

| Property | Type | Description |
|----------|------|-------------|
| `Caption` | string | Item text (use '-' for separator, '&' for hotkey) |
| `Checked` | Boolean | Check mark |
| `Enabled` | Boolean | Enabled state |
| `ShortCut` | TShortCut | Keyboard shortcut |
| `Tag` | Integer | User data |

## File Dialogs

### TOpenDialog

File open dialog.

```pascal
dlg := TOpenDialog.Create(nil);
try
  dlg.Title := 'Select Plugin File';
  dlg.Filter := 'Plugin Files (*.esp;*.esm)|*.esp;*.esm|All Files (*.*)|*.*';
  dlg.FilterIndex := 1;
  dlg.InitialDir := wbDataPath;

  if dlg.Execute then
    AddMessage('Selected: ' + dlg.FileName);
finally
  dlg.Free;
end;
```

| Property | Type | Description |
|----------|------|-------------|
| `FileName` | string | Selected file |
| `Files` | TStrings | Selected files (multi-select) |
| `Filter` | string | File filter |
| `FilterIndex` | Integer | Active filter (1-based) |
| `InitialDir` | string | Initial directory |
| `Title` | string | Dialog title |
| `Options` | TOpenOptions | Dialog options |

**Filter format:**
```pascal
'Description1|*.ext1|Description2|*.ext2'
```

**Options:**
```pascal
ofAllowMultiSelect   // Allow multiple files
ofFileMustExist      // File must exist
ofPathMustExist      // Path must exist
ofOverwritePrompt    // Confirm overwrite
ofHideReadOnly       // Hide read-only checkbox
```

### TSaveDialog

File save dialog.

```pascal
dlg := TSaveDialog.Create(nil);
try
  dlg.Title := 'Save Export';
  dlg.Filter := 'Text Files (*.txt)|*.txt|All Files (*.*)|*.*';
  dlg.DefaultExt := 'txt';
  dlg.FileName := 'export.txt';

  if dlg.Execute then
    AddMessage('Saving to: ' + dlg.FileName);
finally
  dlg.Free;
end;
```

| Property | Type | Description |
|----------|------|-------------|
| `DefaultExt` | string | Default extension (without dot) |

## Complete Form Examples

### Example 1: Record Selector Form

```pascal
// Create form to select records
var
  form: TForm;
  listBox: TListBox;
  btnOK, btnCancel: TButton;
  i: Integer;
  rec: IwbMainRecord;
  selectedEditorID: string;
begin
  form := TForm.Create(nil);
  try
    form.Caption := 'Select Record';
    form.Width := 400;
    form.Height := 500;
    form.Position := poScreenCenter;
    form.BorderStyle := bsDialog;

    // Create list box
    listBox := TListBox.Create(form);
    listBox.Parent := form;
    listBox.Left := 10;
    listBox.Top := 10;
    listBox.Width := form.ClientWidth - 20;
    listBox.Height := form.ClientHeight - 60;

    // Populate list
    for i := 0 to RecordCount(FileByIndex(0)) - 1 do begin
      rec := RecordByIndex(FileByIndex(0), i);
      if rec.Signature = 'NPC_' then
        listBox.Items.AddObject(rec.EditorID, TObject(i));
    end;

    // OK button
    btnOK := TButton.Create(form);
    btnOK.Parent := form;
    btnOK.Caption := 'OK';
    btnOK.Left := form.ClientWidth - 180;
    btnOK.Top := form.ClientHeight - 40;
    btnOK.Width := 80;
    btnOK.Default := True;
    btnOK.ModalResult := mrOk;

    // Cancel button
    btnCancel := TButton.Create(form);
    btnCancel.Parent := form;
    btnCancel.Caption := 'Cancel';
    btnCancel.Left := form.ClientWidth - 90;
    btnCancel.Top := form.ClientHeight - 40;
    btnCancel.Width := 80;
    btnCancel.Cancel := True;
    btnCancel.ModalResult := mrCancel;

    // Show dialog
    if form.ShowModal = mrOk then begin
      if listBox.ItemIndex >= 0 then begin
        selectedEditorID := listBox.Items[listBox.ItemIndex];
        AddMessage('Selected: ' + selectedEditorID);
      end;
    end;
  finally
    form.Free;
  end;
end;
```

### Example 2: Progress Dialog

```pascal
// Show progress while processing
var
  form: TForm;
  lblStatus: TLabel;
  progress: TProgressBar;
  i, total: Integer;
  rec: IwbMainRecord;
begin
  form := TForm.Create(nil);
  try
    form.Caption := 'Processing Records';
    form.Width := 400;
    form.Height := 150;
    form.Position := poScreenCenter;
    form.BorderStyle := bsDialog;

    // Status label
    lblStatus := TLabel.Create(form);
    lblStatus.Parent := form;
    lblStatus.Left := 10;
    lblStatus.Top := 20;
    lblStatus.Caption := 'Processing...';

    // Progress bar
    progress := TProgressBar.Create(form);
    progress.Parent := form;
    progress.Left := 10;
    progress.Top := 50;
    progress.Width := form.ClientWidth - 20;

    // Show form
    form.Show;

    // Process records
    total := RecordCount(FileByIndex(0));
    progress.Max := total;

    for i := 0 to total - 1 do begin
      rec := RecordByIndex(FileByIndex(0), i);

      // Update UI
      lblStatus.Caption := Format('Processing %d of %d: %s',
        [i + 1, total, rec.EditorID]);
      progress.Position := i + 1;
      Application.ProcessMessages;

      // Process record here...
    end;

    ShowMessage('Processing complete!');
  finally
    form.Free;
  end;
end;
```

### Example 3: Configuration Form with Tabs

```pascal
// Multi-tab configuration form
var
  form: TForm;
  pageControl: TPageControl;
  tabGeneral, tabAdvanced: TTabSheet;
  editPrefix: TEdit;
  lblPrefix: TLabel;
  chkIncludeDeleted: TCheckBox;
  btnOK, btnCancel: TButton;
begin
  form := TForm.Create(nil);
  try
    form.Caption := 'Export Configuration';
    form.Width := 500;
    form.Height := 400;
    form.Position := poScreenCenter;

    // Page control
    pageControl := TPageControl.Create(form);
    pageControl.Parent := form;
    pageControl.Left := 10;
    pageControl.Top := 10;
    pageControl.Width := form.ClientWidth - 20;
    pageControl.Height := form.ClientHeight - 60;

    // General tab
    tabGeneral := TTabSheet.Create(pageControl);
    tabGeneral.PageControl := pageControl;
    tabGeneral.Caption := 'General';

    lblPrefix := TLabel.Create(tabGeneral);
    lblPrefix.Parent := tabGeneral;
    lblPrefix.Left := 10;
    lblPrefix.Top := 20;
    lblPrefix.Caption := 'EditorID Prefix:';

    editPrefix := TEdit.Create(tabGeneral);
    editPrefix.Parent := tabGeneral;
    editPrefix.Left := 10;
    editPrefix.Top := 40;
    editPrefix.Width := 200;
    editPrefix.Text := 'MyMod_';

    // Advanced tab
    tabAdvanced := TTabSheet.Create(pageControl);
    tabAdvanced.PageControl := pageControl;
    tabAdvanced.Caption := 'Advanced';

    chkIncludeDeleted := TCheckBox.Create(tabAdvanced);
    chkIncludeDeleted.Parent := tabAdvanced;
    chkIncludeDeleted.Left := 10;
    chkIncludeDeleted.Top := 20;
    chkIncludeDeleted.Caption := 'Include deleted records';

    // Buttons
    btnOK := TButton.Create(form);
    btnOK.Parent := form;
    btnOK.Caption := 'OK';
    btnOK.Left := form.ClientWidth - 180;
    btnOK.Top := form.ClientHeight - 40;
    btnOK.ModalResult := mrOk;

    btnCancel := TButton.Create(form);
    btnCancel.Parent := form;
    btnCancel.Caption := 'Cancel';
    btnCancel.Left := form.ClientWidth - 90;
    btnCancel.Top := form.ClientHeight - 40;
    btnCancel.ModalResult := mrCancel;

    // Show and get results
    if form.ShowModal = mrOk then begin
      AddMessage('Prefix: ' + editPrefix.Text);
      AddMessage('Include deleted: ' + BoolToStr(chkIncludeDeleted.Checked, True));
    end;
  finally
    form.Free;
  end;
end;
```

---

[← Back to Standard Library Overview](stdlib_home.md) | [Next: Graphics & Drawing →](stdlib_graphics.md)
