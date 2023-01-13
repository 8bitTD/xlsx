# xlsx
## windows only

## example
```
/*
[dependencies]
dirs = "3.0"
chrono = "*"
xlsx = { git = "https://github.com/8bitTD/xlsx", branch = "main"}
*/
fn main() {
    let dt_path= dirs::desktop_dir().unwrap().as_os_str().to_str().unwrap().to_string().replace("\\","/");
    let datetime = chrono::Utc::now().with_timezone(&chrono::FixedOffset::east_opt(9 * 3600).unwrap()).naive_local();
    let xlsx_path = format!("{}{}{}{}",dt_path,"/test_",datetime.format("%Y%m%d%H%M%S").to_string(), ".xlsx");
    let mut cells = Vec::new();
    let c = xlsx::Cell::default().set_pos(1,1).set_content("_test");
    cells.push(c);
    let sheet1 = xlsx::Sheet::default()
        .set_name("test_sheet")
        .set_cells(cells);
    let mut xlsx = xlsx::Xlsx::default().add_sheet(sheet1).set_path(xlsx_path);
    xlsx.export_xlsx();
    while xlsx.is_exec(){
        xlsx.update();
    }
}
```
