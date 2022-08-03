# xlsx


```
fn main() {
    let mut cells = Vec::new();
    let c = xlsx::Cell::default().set_pos(1,1).set_content("aaa");
    cells.push(c);
    let c = xlsx::Cell::default().set_pos(1,2).set_content("bbbb");
    cells.push(c);
    let c = xlsx::Cell::default().set_pos(1,3).set_content("ccccc");
    cells.push(c);

    let sheet = xlsx::Sheet::default()
        .set_name("sheet_name")
        .set_cells(cells)
        .add_width(1,5)
        .add_width(2,80)
        .add_width(3,10)
        .add_line(1,1,1,3,1);
    let mut xlsx = xlsx::Xlsx::default().add_sheet(sheet);
    xlsx.export_xlsx();
    while xlsx.is_exec(){
        xlsx.update();
    }
}
```
