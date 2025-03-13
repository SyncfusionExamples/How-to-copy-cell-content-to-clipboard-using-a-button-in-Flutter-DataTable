# How to copy cell content to clipboard using a button in Flutter DataTable (SfDataGrid)?.

In this article, we will show you how to copy cell content to clipboard using a button in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) with the necessary properties. The [DataGridSource.rows](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/rows.html) property provides access to all rows in the grid. To copy the data, iterate through each row in DataGridSource.rows and extract the values of each cell. Format the data as a tab-separated string to maintain the table structure. Finally, use Flutter’s [Clipboard.setData](https://api.flutter.dev/flutter/services/Clipboard/setData.html) method to copy the formatted string to the clipboard, allowing them to paste the copied content anywhere.

```dart
void copyEntireGrid(EmployeeDataSource dataSource) {
    String copiedData = '';

    // Extract column headers
    copiedData += 'ID\tName\tDesignation\tSalary\n';

    // Extract row data
    copiedData += dataSource.rows
        .map((row) {
          return row.getCells().map((cell) => cell.value.toString()).join('\t');
        })
        .join('\n');

    Clipboard.setData(ClipboardData(text: copiedData));
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Syncfusion Flutter DataGrid'),
        actions: [
          IconButton(
            icon: const Icon(Icons.copy),
            tooltip: 'Copy DataGrid',
            onPressed: () {
              copyEntireGrid(employeeDataSource);
            },
          ),
        ],
      ),
      body: SfDataGrid(
        source: employeeDataSource,
        shrinkWrapRows: true,
        columnWidthMode: ColumnWidthMode.fill,
        columns: <GridColumn>[
          GridColumn(
            columnName: 'id',
            label: Container(
              padding: const EdgeInsets.all(16.0),
              alignment: Alignment.center,
              child: const Text('ID'),
            ),
          ),
          GridColumn(
            columnName: 'name',
            label: Container(
              padding: const EdgeInsets.all(8.0),
              alignment: Alignment.center,
              child: const Text('Name'),
            ),
          ),
          GridColumn(
            columnName: 'designation',
            label: Container(
              padding: const EdgeInsets.all(8.0),
              alignment: Alignment.center,
              child: const Text('Designation', overflow: TextOverflow.ellipsis),
            ),
          ),
          GridColumn(
            columnName: 'salary',
            label: Container(
              padding: const EdgeInsets.all(8.0),
              alignment: Alignment.center,
              child: const Text('Salary'),
            ),
          ),
        ],
      ),
    );
  }
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-copy-cell-content-to-clipboard-using-a-button-in-Flutter-DataTable).