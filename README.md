- Set default options
```js
Tabulator.defaultOptions.layout = "fitColumns";
Tabulator.defaultOptions.movableColumns = true;
Tabulator.defaultOptions.columnDefaults = {
  headerHozAlign: "center",
  hozAlign: "left",
  vertAlign: "middle",
  headerSort: false,
};
```

- Create table
```js
const container = document.getElementById("container");
let table;

table = new Tabulator(container, {
  height: "100%",
  data: [],
  index: "id", // id
  rowHeight: 25, // default 25
  initialSort: [
    {column: "id", dir: "asc"},
    {column: "createdAt", dir: "asc"},
  ],
  columns: [
    {
      title: "ID",
      field: "id",
      sorter: "number",
    }, {
      title: "CreatedAt",
      field: "createdAt",
      formatter: function(cell, formatterParams, onRendered) {
        const v = cell.getValue();
        if (!v) {
          return "";
        }
        return moment(v).format("LLLL");
      },
    }
  [
});

await table.addData([
  {
    id: 1,
    createdAt: Date.now()
  }, {
    id: 2,
    createdAt: Date.now()
  }
]}

```
