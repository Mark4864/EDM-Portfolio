let
    Source = Csv.Document(File.Contents("C:\Users\COMLAB\Downloads\Data\Uncleaned_DS_jobs.csv"),[Delimiter=",", Columns=15, Encoding=1252, QuoteStyle=QuoteStyle.Csv]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"index", Int64.Type}, {"Job Title", type text}, {"Salary Estimate", type text}, {"Job Description", type text}, {"Rating", type number}, {"Company Name", type text}, {"Location", type text}, {"Headquarters", type text}, {"Size", type text}, {"Founded", Int64.Type}, {"Type of ownership", type text}, {"Industry", type text}, {"Sector", type text}, {"Revenue", type text}, {"Competitors", type text}}),
    #"Extracted Text Before Delimiter" = Table.TransformColumns(#"Changed Type", {{"Salary Estimate", each Text.BeforeDelimiter(_, "("), type text}}),
    #"Sorted Rows" = Table.Sort(#"Extracted Text Before Delimiter",{{"Salary Estimate", Order.Ascending}}),
    #"Inserted Text Between Delimiters" = Table.AddColumn(#"Sorted Rows", "Min Salary", each Text.BetweenDelimiters([Salary Estimate], "$", "K"), type text),
    #"Inserted Text Between Delimiters1" = Table.AddColumn(#"Inserted Text Between Delimiters", "Max Salary", each Text.BetweenDelimiters([Salary Estimate], "$", "K", 1, 0), type text),
    #"Added Custom" = Table.AddColumn(#"Inserted Text Between Delimiters1", "Role Type", each if Text.Contains([Job Title], "Data Scientist") then
"Data Scientist"
else if Text.Contains([Job Title], "Data Analyst") then
"Data Analyst"
else if Text.Contains([Job Title], "Data Engineer") then
"Data Engineer"

else if Text.Contains([Job Title], "Machine Learning") then
"Machine Learning Engineer"
else
"other"),
    #"Changed Type1" = Table.TransformColumnTypes(#"Added Custom",{{"Role Type", type text}}),
    #"Split Column by Delimiter" = Table.SplitColumn(#"Changed Type1", "Location", Splitter.SplitTextByDelimiter(",", QuoteStyle.Csv), {"Location.1", "Location.2"}),
    #"Changed Type2" = Table.TransformColumnTypes(#"Split Column by Delimiter",{{"Location.1", type text}, {"Location.2", type text}}),
    #"Replaced Value" = Table.ReplaceValue(#"Changed Type2","Anne Rundell","MA",Replacer.ReplaceText,{"Location.2"}),
    #"Renamed Columns" = Table.RenameColumns(#"Replaced Value",{{"Location.2", "State Abbreviations"}, {"Location.1", "Location"}}),
    #"Inserted Text Before Delimiter" = Table.AddColumn(#"Renamed Columns", "MinCompanySize", each Text.BeforeDelimiter([Size], " "), type text),
    #"Inserted Text Between Delimiters2" = Table.AddColumn(#"Inserted Text Before Delimiter", "Text Between Delimiters", each Text.BetweenDelimiters([Size], " ", " ", 1, 0), type text),
    #"Renamed Columns1" = Table.RenameColumns(#"Inserted Text Between Delimiters2",{{"Text Between Delimiters", "MaxCompanySize"}}),
    #"Filtered Rows" = Table.SelectRows(#"Renamed Columns1", each ([Competitors] <> "-1") and ([Revenue] <> "Unknown / Non-Applicable") and ([Industry] <> "-1")),
    #"Split Column by Delimiter1" = Table.SplitColumn(#"Filtered Rows", "Company Name", Splitter.SplitTextByDelimiter("#(lf)", QuoteStyle.Csv), {"Company Name.1", "Company Name.2"}),
    #"Changed Type3" = Table.TransformColumnTypes(#"Split Column by Delimiter1",{{"Company Name.1", type text}, {"Company Name.2", type number}}),
    #"Removed Columns" = Table.RemoveColumns(#"Changed Type3",{"Company Name.2"}),
    #"Renamed Columns2" = Table.RenameColumns(#"Removed Columns",{{"Company Name.1", "Company Name"}})
in
    #"Renamed Columns2"
