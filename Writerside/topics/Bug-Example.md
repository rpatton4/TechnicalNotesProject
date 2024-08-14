# Bug Example

`awk 'BEGIN{FS=",";RS="\r\n";s1="\"";OFS="\",\""} {$1=$1;$0=s1 $0 s1} 1' <input file> > <output file>`

