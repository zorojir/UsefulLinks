# UsefulLinks
http://www.geekzilla.co.uk/View00FF7904-B510-468C-A2C8-F859AA20581F.htm



<style type="text/css">body{margin:40px auto;max-width:650px;line-height:1.6;font-size:18px;color:#444;padding:0 10px}h1,h2,h3{line-height:1.2}
</style>





UiPath has released the 2019 LTS Version (2019.10.1).

Details of the release can be found here : https://docs.uipath.com/releasenotes/docs/2019-10-1

Platform Installer Download Link: https://download.uipath.com/UiPathPlatformInstaller.exe (712 MB)

All the documentation sections (Studio/Robot/Orchestrator) are also updated with details of each new feature added.


http://download.uipath.com/versions/19.10.6/UiPathOrchestrator.msi



(From dr1 in DT.AsEnumerable() Select Newdt.LoadDataRow(New Object() {dr1(“Whs”).ToString, Cint(dr1(“FL”).toString)},false)).CopyToDataTable


# To Get Matched Records

Datatable Out_Matched_Data = In_DataTable1.AsEnumerable().Where(function(row) In_DataTable2.AsEnumerable().Select(function(r) r.Field(Of Int32)(In_DT2_ColName_To_Match.ToString)).Any(function(x) x = row.Field(Of Int32)(In_DT1_ColName_To_Match.ToString))).CopyToDataTable()

# To Get Not Matched Records

Datatable Out_NonMatched_Data = In_DataTable1.AsEnumerable().Where(function(row) Not In_DataTable2.AsEnumerable().Select(function(r) r.Field(Of Int32)(In_DT2_ColName_To_Match.ToString)).Any(function(x) x = row.Field(Of Int32)(In_DT1_ColName_To_Match.ToString))).CopyToDataTable()

#  Refer the below code to remove the empty row from the Data Table.

DataTableName=DataTableName.Rows.Cast(Of DataRow)().Where(Function(row) Not row.ItemArray.All(Function(field) field Is DBNull.Value Or field.Equals(""))).CopyToDataTable()


#  to find sum based on condition

dtTesting.AsEnumerable.Sum(Function (x) If(Double.TryParse(x.item("Column2").ToString, Nothing), Double.Parse(x.Item("Column2").ToString), 0))


#  to find sum of a column without condition
Dt.AsEnumerable().Sum(Function(x) Double.Parse(x.Item(5).ToString))

#  to get duplicate
datatable variable** (From p in dt.Select() where( From q in dt.Select() where string.Join(",",q.ItemArray).Equals(string.Join(",",p.ItemArray)) Select q).ToArray.Count>1 Select p).ToArray.CopyToDataTable

#  Remove rows based on particular column is empty.
DataTableName.Select("Convert(column3, System.String)< >''").CopyToDataTable()
or
DataTableName.Select("column3< >''").CopyToDataTable()

# Distinct Based on the specific column name from the data table and need to return the whole data.
Remove Duplicate record from the Data Table based on Column Name
dt.AsEnumerable().GroupBy(Function(i) i.Field(Of String)("ColumnName")).Select(Function(g) g.First).CopyToDataTable()
Or
((From LineNo In dt.DefaultView.ToTable(True,"Product").Select().ToList() Select (From row In dt.Select Where row("Product").ToString=LineNo("Product").ToString Select row).ToList(0)).ToList()).CopyToDatatable()

#  Distinct Based on the specific column name from the data table.

DataView view = new DataView(table)
DataTable distinctValues = view.ToTable(true, "Column1", "Column2" ...)
or
DataTable =DataTable.DefaultView.ToTable(true)

Sorting the data table based on particular column name
dt = dt.Select("",[ColumnName] asc").CopyToDataTable()

# Duplicate records from the same data table
(From p in dt.Select() where( From q in dt.Select() where string.Join(",",q.ItemArray).Equals(string.Join(",",p.ItemArray)) Select q).ToArray.Count>1 Select p).ToArray.CopyToDataTable()

# Duplicate records from the same data table and
If you want specific Column alone mention the column name
(From p in dt.Select() where( From q in dt.Select() where q("ColumnName").Equals(p("ColumnName")) Select q).ToArray.Count>1 Select p).ToArray.CopyToDataTable()

# Get Max value from the data table column value
int MaxValue=Convert.ToInt32(dt.AsEnumerable().Max(Function(row) row("Column2")))


# find a value in an array and get the value
(from name in febaFiles where name.Contains("At") select name).First.ToString


# regex to remove hidden characters in a string

System.Text.RegularExpressions.Regex.Replace(Input variable, "[^\x20-\x7F]", "")

# groupby or groupby and calculate sum

datatable dta

First group the datatable based on ID by using below Query and assign it to dt1
dt1=(From p In dta.Select()
Group p by ID=p.Item(“ID”).ToString Into Group
Select Group(0)).ToArray.CopyToDataTable()

Now take only two columns by using below query
dt1=dt1.DefaultView.ToTable(False,“ID”,“Name”)

Now Add one datacolumn to dt1 by using add datacolumn activity and give name Amount to that column

Then create one list of strings ListA

Then use this query
ListA=(From p In dta.Select()
Group p By ID=p.Item(“ID”).ToString Into GroupA=Group
Select Convert.ToString(GroupA.Sum(Function(x) Convert.ToDouble(x.Item(“Amount”).ToString)))).ToList()

Next Run one Foreach loop for dt1

Inside for each use one assign activity
row(“Amount”)=ListA(dt1.Rows.IndexOf(row)).ToString

# Group by without sum
(From p In DT.AsEnumerable() Group By x= New With { Key.a =p.Item("id"),Key.b=p.Item("name")} Into Group Select Group(0)).ToArray().CopyToDataTable()

# group by some condition , here the condition is amount column should be empty
(From p In DT.AsEnumerable().Where(function(x) string.IsNullOrEmpty(x("amount").ToString)) Group By x= New With { Key.a =p.Item("id"),Key.b=p.Item("name")} Into Group Select Group(0)).ToArray().CopyToDataTable()
