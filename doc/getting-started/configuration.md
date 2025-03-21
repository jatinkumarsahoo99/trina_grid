# Configuration

TrinaGrid offers extensive configuration options to customize its appearance and behavior. This guide covers the main configuration options available.

## TrinaGridConfiguration

The `TrinaGridConfiguration` class is the main way to configure TrinaGrid. You can pass it to the `configuration` parameter of the `TrinaGrid` widget:

```dart
TrinaGrid(
  columns: columns,
  rows: rows,
  configuration: TrinaGridConfiguration(
    // Configuration options here
  ),
)
```

## Basic Configuration

### Style Configuration

The `style` property allows you to customize the visual appearance of the grid:

```dart
TrinaGridConfiguration(
  style: TrinaGridStyleConfig(
    // Colors
    gridBackgroundColor: Colors.white,
    borderColor: Colors.grey[300]!,
    activatedBorderColor: Colors.blue,
    activatedColor: Colors.blue.withOpacity(0.2),
    inactivatedBorderColor: Colors.grey[300]!,
    
    // Cell styles
    cellColorInEditState: Colors.white,
    cellColorInReadOnlyState: Colors.grey[200]!,
    
    // Text styles
    columnTextStyle: TextStyle(
      color: Colors.black,
      fontSize: 14,
      fontWeight: FontWeight.w600,
    ),
    cellTextStyle: TextStyle(
      color: Colors.black,
      fontSize: 14,
    ),
    
    // Sizes
    rowHeight: 45,
    columnHeight: 45,
    columnFilterHeight: 45,
    
    // Icons
    iconSize: 18,
    iconColor: Colors.black54,
    
    // Even/odd row colors
    oddRowColor: Colors.grey[100],
    evenRowColor: Colors.white,
  ),
)
```

### Scrollbar Configuration

Configure the scrollbars with the `scrollbar` property for general scrollbar behavior:

```dart
TrinaGridConfiguration(
  scrollbar: TrinaGridScrollbarConfig(
    isAlwaysShown: true,
    thickness: 8,
    hoverThickness: 10,
    scrollBarColor: Colors.grey[600]!,
    scrollBarTrackColor: Colors.grey[100]!,
  ),
)
```

For more detailed control over the grid's scrollbars, you can use the `scrollbarConfig` extension property which provides additional customization options:

```dart
TrinaGridConfiguration(
  // General scrollbar behavior
  scrollbar: TrinaGridScrollbarConfig(
    isAlwaysShown: true,
    draggableScrollbar: true,
  ),
  // The scrollbarConfig extension provides access to the custom scrollbar settings
).scrollbarConfig = TrinaScrollbarConfig(
  // Control visibility
  visible: true,
  showTrack: true,
  showHorizontal: true,
  showVertical: true,
  
  // Appearance
  thickness: 8.0,
  minThumbLength: 40.0,
  thumbColor: Colors.grey.withOpacity(0.6),
  trackColor: Colors.grey.withOpacity(0.2),
);
```

The `TrinaScrollbarConfig` provides the following options:

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `visible` | `bool` | `true` | Whether the scrollbar thumb is visible |
| `showTrack` | `bool` | `true` | Whether to show the scrollbar track |
| `showHorizontal` | `bool` | `true` | Whether to show the horizontal scrollbar |
| `showVertical` | `bool` | `true` | Whether to show the vertical scrollbar |
| `thickness` | `double` | `8.0` | Thickness of the scrollbar |
| `minThumbLength` | `double` | `40.0` | Minimum length of the scrollbar thumb |
| `thumbColor` | `Color?` | `Colors.grey.withOpacity(0.6)` | Color of the scrollbar thumb |
| `trackColor` | `Color?` | `Colors.grey.withOpacity(0.2)` | Color of the scrollbar track |

### Column Configuration

Set default column behavior:

```dart
TrinaGridConfiguration(
  columnSize: TrinaGridColumnSizeConfig(
    autoSizeMode: TrinaAutoSizeMode.scale,
    resizeMode: TrinaResizeMode.normal,
  ),
)
```

## Behavior Configuration

### Selection Mode

Configure how cells or rows can be selected:

```dart
TrinaGridConfiguration(
  selectingMode: TrinaGridSelectingMode.cell, // or row, none
)
```

### Editing Configuration

Control editing behavior:

```dart
TrinaGridConfiguration(
  enableMoveDownAfterSelecting: true,
  enterKeyAction: TrinaGridEnterKeyAction.editingAndMoveDown,
  enableEditingMode: true,
)
```

### Keyboard Navigation

Configure keyboard shortcuts:

```dart
TrinaGridConfiguration(
  shortcut: TrinaGridShortcut(
    actions: {
      // Custom shortcuts
      LogicalKeySet(LogicalKeyboardKey.control, LogicalKeyboardKey.keyA): 
          TrinaGridShortcutAction.selectAll,
    },
  ),
)
```

## Predefined Configurations

TrinaGrid provides some predefined configurations:

### Dark Mode

```dart
TrinaGrid(
  columns: columns,
  rows: rows,
  configuration: TrinaGridConfiguration.dark(),
)
```

### Custom Theme

You can create your own theme by extending the default configuration:

```dart
final myTheme = TrinaGridConfiguration(
  style: TrinaGridStyleConfig(
    gridBackgroundColor: Colors.indigo[50]!,
    borderColor: Colors.indigo[300]!,
    activatedBorderColor: Colors.indigo,
    activatedColor: Colors.indigo.withOpacity(0.2),
    columnTextStyle: const TextStyle(
      color: Colors.indigo[900]!,
      fontWeight: FontWeight.bold,
    ),
    cellTextStyle: TextStyle(
      color: Colors.indigo[900]!,
    ),
    iconColor: Colors.indigo,
  ),
);

TrinaGrid(
  columns: columns,
  rows: rows,
  configuration: myTheme,
)
```

## Column-Specific Configuration

Many configuration options can be set at the column level, which will override the global configuration:

```dart
TrinaColumn(
  title: 'Name',
  field: 'name',
  type: TrinaColumnType.text(),
  width: 200,
  // Column-specific configuration
  textAlign: TrinaColumnTextAlign.center,
  titleTextAlign: TrinaColumnTextAlign.center,
  enableSorting: true,
  enableFilterMenuItem: true,
  enableContextMenu: true,
  enableDropToResize: true,
  enableRowDrag: false,
  enableRowChecked: false,
  enableEditingMode: true,
  readOnly: false,
)
```

## Row-Specific Configuration

Rows can also have specific configurations:

```dart
TrinaRow(
  cells: {
    'id': TrinaCell(value: '1'),
    'name': TrinaCell(value: 'John Doe'),
  },
  // Row-specific configuration
  checked: true,
  type: TrinaRowType.normal(), // or group
)
```

## Cell-Specific Configuration

Individual cells can have their own configuration:

```dart
TrinaCell(
  value: 'John Doe',
  // Cell-specific configuration
  renderer: (context) => Text(
    context.cell.value.toString(),
    style: const TextStyle(fontWeight: FontWeight.bold),
  ),
)
```

## Complete Configuration Example

Here's a complete example showing various configuration options:

```dart
TrinaGrid(
  columns: columns,
  rows: rows,
  onLoaded: (TrinaGridOnLoadedEvent event) {
    stateManager = event.stateManager;
  },
  configuration: TrinaGridConfiguration(
    // Style configuration
    style: TrinaGridStyleConfig(
      gridBackgroundColor: Colors.white,
      borderColor: Colors.grey[300]!,
      activatedBorderColor: Colors.blue,
      activatedColor: Colors.blue.withOpacity(0.2),
      cellTextStyle: const TextStyle(fontSize: 14),
      columnTextStyle: const TextStyle(
        fontSize: 14,
        fontWeight: FontWeight.bold,
      ),
      rowHeight: 45,
      columnHeight: 45,
      iconSize: 18,
      iconColor: Colors.blue,
      enableCellBorderHorizontal: true,
      enableCellBorderVertical: true,
      gridBorderRadius: BorderRadius.circular(8),
      gridPopupBorderRadius: BorderRadius.circular(8),
      enableGridBorderShadow: true,
      oddRowColor: Colors.grey[100],
      evenRowColor: Colors.white,
    ),
    
    // Scrollbar configuration
    scrollbar: const TrinaGridScrollbarConfig(
      isAlwaysShown: true,
      thickness: 8,
      hoverThickness: 10,
    ),
    
    // Custom scrollbar appearance
    // Access through the scrollbarConfig extension
    // scrollbarConfig: TrinaScrollbarConfig(
    //   visible: true,
    //   showTrack: true,
    //   showHorizontal: true,
    //   showVertical: true,
    //   thickness: 8.0,
    //   minThumbLength: 40.0,
    //   thumbColor: Colors.blue.withOpacity(0.6),
    //   trackColor: Colors.grey.withOpacity(0.2),
    // ),
    
    // Column configuration
    columnSize: const TrinaGridColumnSizeConfig(
      autoSizeMode: TrinaAutoSizeMode.scale,
      resizeMode: TrinaResizeMode.normal,
    ),
    
    // Behavior configuration
    enableMoveDownAfterSelecting: true,
    enterKeyAction: TrinaGridEnterKeyAction.editingAndMoveDown,
    enableEditingMode: true,
    selectingMode: TrinaGridSelectingMode.cell,
    
    // Keyboard shortcuts
    shortcut: TrinaGridShortcut(
      actions: {
        LogicalKeySet(LogicalKeyboardKey.control, LogicalKeyboardKey.keyA): 
            TrinaGridShortcutAction.selectAll,
      },
    ),
  ),
)
```

## Next Steps

- [Column Types](../features/column-types.md)
- [Cell Renderers](../features/cell-renderer.md)
- [Custom Styling](../features/custom-styling.md)
