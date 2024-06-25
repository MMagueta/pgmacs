# Changelog


## [0.8] - Unreleased

- Look and feel: adopt the button faces used by Emacs’ customization support.

- New widgets to allow widget-based editing of a PostgreSQL JSON or JSONB value, a DATE values and
  UUID values.

- When displaying a table, show whether row-level security is enabled for this table.

- Row deletion is now executed in an SQL transaction. If the number of affected rows is not equal to
  1 (indicating a logic error in our code), then the transaction is rolled back.

- A `Count rows` button is displayed in table row-list buffers.

- The connection widget uses initial values for database name, username, hostname and password taken
  from environment variables such as `POSTGRES_DATABASE` and `POSTGRES_USER`, if defined.


## [0.7] - 2024-05-23

- Fix bug in `e` keybinding (`pgmacs-run-sql`) when outside a table.

- `pgmacs-run-sql`: allow for SQL commands that produce no output rows.

- In a row-list, new keybindings for digits that move point to the nth column of the table, counting
  from zero. For example, pressing `2` moves point to the third column.

- In a row-list, new `v` keybinding displays the column value at point (which may be truncated) in a
  dedicated (readonly) buffer.

- Fix bug in the the widget-based editing functionality, which was discarding edits.

- New widget to allow widget-based editing of a PostgreSQL HSTORE value, which is represented in
  Emacs Lisp as a hashtable.


## [0.6] - 2024-05-09

- New keybinding in the table-list buffer: `r` allows you to rename the table at point.

- New keybinding in the table-list buffer: `g` refreshes the table list display by retrieving all
  the table metainformation again.

- Improve the display of NULL column values.


## [0.5] - 2024-04-27

- Information on available and installed PostgreSQL extensions is included in the buffer generated
  by `pgmacs--display-backend-information`.

- API change: `pgmacs-open/string` and `pgmacs-open/uri` renamed to `pgmacs-open-string` and
  `pgmacs-open-uri` to follow the conservative Emacs Lisp style guide.


## [0.4] - 2024-04-05

- The row count shown in the list-of-tables buffer is now precise even when the tables have not been
  VACUUMed. This precision is at the cost of speed on large tables (calculated with `COUNT(*)`).

- Add `h` keybinding in row-list and table-list buffers that show a buffer with the main keybindings.

- New keybindings `<` and `>` in row-list and table-list buffers to move to the beginning and the
  end of the vtable, respectively.


## [0.3] - 2024-03-31

- The comment on a table can be modified by pressing `RET` in the list-of-tables buffer.

- Alignment of table headers should be improved, both in a window system and a terminal.

- New keybinding for `<delete>` and `<backspace>` in the list-of-tables buffer, which allow easy
  deletion of tables after `yes-or-no-p` confirmation.


## [0.2] - 2024-03-29

- New functions `pgmacs-open/string` to open PGmacs with a PostgreSQL connection string, and
  `pgmacs-open/uri` to open PGmacs with a PostgreSQL connection URI.
  
- New function `pgmacs` which opens a widget-based buffer to enter PostgreSQL connection information.

- `e` in keymap reads an SQL query from the minibuffer and displays the output in a temporary buffer.

- `j` in a table view copies the current row to the kill ring in JSON format.

- Pressing `k` in a table view copies the current row to a special kill ring. Pressing `y` then
  pastes the copied row into the table, taking care to use defaults for any colums for which a
  schema-specified default value is defined.

- In a table view for which pagination is active (only a subset of the table/query contents are
  displayed in the buffer), pressing `n` and `p` updates the table data to display the next and
  previous pages respectively.

- Pressing `+` in a table view allows you to insert a new row, with values for each column entered
  in the minibuffer. Columns for which an SQL default value is specified will use that default
  value.
  
- Pressing `i` in a table view allows you to insert a new row, with values for each column entered
  in a widget-based buffer. Columns for which an SQL default value is specified will use that default
  value.

- In table buffers, include a button that dumps the table as CSV to an Emacs buffer.

- Faces `pgmacs-table-header` and `pgmacs-table-data` are used to display the header and the rows of
  database tables.
  
- Variable `pgmacs-row-colors` specifies the colors used for alternating rows in a database table.

- Variable `pgmacs-row-limit` specifies the maximum number of rows to retrieve per database query,
  before results are paginated.

- Support for schema-qualified tables in the table list, with an updated version of the pg-el
  library.

- Some attempt to show query progress on slow connections to PostgreSQL using Emacs's
  `make-progress-reporter` functionality.
