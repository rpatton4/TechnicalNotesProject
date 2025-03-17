# CSV Processing

## Surrounding fields with double-quotes
``awk 'BEGIN{FS=",";RS="\r\n";s1="\"";OFS="\",\""} {$1=$1;$0=s1 $0 s1} 1' <input file> > <output file>``

This may pick up a weird 1st character from Excel or something,
and it may add an empty final line

https://stackoverflow.com/questions/61803736/script-that-add-double-quotes-to-every-column-in-csv-file-problem

## Converting commas to tabs  
`awk -F ',' 'BEGIN {OFS="\t"} {$1=$1}1' <input.csv> <output.txt>`