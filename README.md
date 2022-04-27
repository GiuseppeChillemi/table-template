# table-template
Template for table style

To enable table style:
```
tbl: #include %table-template.red
style 'table tbl
```
After that table style can be used in layout, as e.g.
```
view [table]
```
This will create an empty table with default size of 317x217 and grid 3x8. Default cell size is 100x25. Both vertial and horizontal scrollers are always included. Scrollers are 17 points thick.

Specifying size for table will fill the extra space with additional cells.
```
view [table 717x517]]
```
This will create an empty table with 7x20 grid.

Grid size of table can be specified separately, e.g.
```
view [table 717x517 data 10x50 options [auto-index: #[true]]
```
When `auto-index` is set to `true` an extra column will be created, automatically enumerated. By this the original order of rows can be restored whenever necessary.
This will create table with eleven columns (10 requested + 1 auto-index) and 50 rows, but in previous boundaries.

When instead of grid size a block is presented as data, this block is interpreted as table. Block should consist of row blocks of equal size. E.g.
```
view [table 717x517 data [["" A B][1 First Row][2 Second Row]]]
```
Values are formed to be presented in table.

Instead of giving data directly as block, file name or url may be specified, to be loaded as table, e.g.
```
view [
    table 717x515 
    data https://support.staffbase.com/hc/en-us/article_attachments/360009197011/username-password-recovery-code.csv 
    options [delimiter: #";"]
]
```
Non-standard delimiter (standard is comma) can currently be specified for urls only.

If you have set up sqlite, data source may be specified as sql query, e.g.
```
sql-query: func [sql][
    out: copy ""
    call/output rejoin [{sqlite3 -csv -header C:\Users\Toomas\sqlite\chinook.db "} sql {"}]  out
    load/as out 'csv
]
view [
    table 717x517 with [
        data: sql-query "select TrackId, Name, Title, Composer from tracks inner join albums on tracks.AlbumID = albums.AlbumId"
    ]
]
```

## Features

Row and column sizes can be changed by dragging on cell border. If holding down control while dragging, sizes of all following rows/columns will be changed too. If ctrl-dragging on first row/column, default size is changed.

Scrolling, wheeling, navigation by keys, sorting, filtering, freezing, copying/pasting, editing -- see local menu
