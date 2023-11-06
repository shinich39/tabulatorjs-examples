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
  rowFormatter: function(row) {
    const element = row.getElement();
    const record = row.getData();
    if (record.createdAt < Date.now()) {
      element.style.backgroundColor = "red";
    } else {
      element.style.backgroundColor = "";
    }
  },
  rowContextMenu: function(e, row) {
    const menu = [];

    menu.push({
      label: "Test",
      menu: [{
        label: "Test",
        action: function(e row) {
          
        }
      }],
    });

    return menu;
  },
  columns: [
    {
      title: "ID",
      field: "id",
      sorter: "number",
    }, {
      title: "CreatedAt",
      field: "createdAt",
      formatter: function(cell, formatterParams, onRendered) {
        const row = cell.getRow();
        const record = row.getData();
        const createdAt = cell.getValue();
        if (!createdAt) {
          return "";
        }
        return moment(createdAt).format("LLLL");
      },
    }
  [
});
```
- Add record
```js
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
- Clear header filter
```js
const columns = table.getColumns();
for (const column of columns) {
  column.setHeaderFilterValue(null);
}
```
- Reload header filter
```js
const columns = table.getColumns();
for (const column of columns) {
  const tmp = column.getHeaderFilterValue();
  if (typeof(tmp) !== "undefined" && tmp !== null) {
    column.setHeaderFilterValue(null);
    column.setHeaderFilterValue(tmp);
  }
}
```
- Re-sort table
```js
const sorters = table.getSorters();
table.setSort(sorters);
```
